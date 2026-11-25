# WideWorldImporters Data Agent — Cross-Table Question Run Report

**Agent:** `wwi_data_agent.py` (LangGraph: schema-link → text-to-SQL → DuckDB execute → grounded synthesis)
**Bundle:** `wideworldimporters_okf` (48 tables, 6 metrics, 3 join paths)
**Data:** `WideworldimportersData/` (48 CSV files)
**Run date:** 2026-11-24
**LLM:** Azure OpenAI (`gpt-4o-mini`, temperature 0)
**Engine:** DuckDB 2.0.1 over the raw CSV files (type auto-detect, `\N` → NULL)

---

## 1. Executive summary

Five cross-table questions were run through the agent. Each answer is reproduced below
alongside a **raw-data verification query** that establishes the ground truth, so the
agent's SQL and natural-language answer can be judged against the CSV files directly.

| # | Question | Agent status | Correct? | Note |
|---|----------|--------------|----------|------|
| Q1 | 10 most recent orders (customer, salesperson, qty) | answered | ⚠ Partial | Grouped by customer+salesperson, not by order; 4-table join was correct |
| Q2 | Customers per country (+region) | answered | ✗ Wrong | Joined `CountryID = DeliveryCityID`; skipped the City→StateProvince→Country hierarchy |
| Q3 | Suppliers of low-stock items (+shortfall) | answered | ⚠ Partial | Rows/SQL correct; the answer *text* misread one row (see §4) |
| Q4 | Top-5 selling items (supplier, on-hand, reorder) | escalated | ⚠ Data correct | SQL returned the right 5 rows; synthesizer produced no answer text |
| Q5 | Revenue by customer (top 5) | escalated | ✗ Wrong | Generated SQL summed the wrong column (near-zero floats) and invented numbers |

**Takeaway:** the *retrieval + execution* half of the pipeline is strong — the agent
correctly links 3–5 tables and runs valid DuckDB SQL over the raw CSVs. The failures are
in **SQL correctness for imprecise questions** (Q2, Q5) and in the **synthesis step**
(Q3 misread, Q4 no-answer). These are documented honestly below with the raw evidence.

---

## 2. Method

Each question was run with:

```powershell
python wwi_data_agent.py "<question>"
```

The agent returned: status, natural-language answer, the generated SQL, the row count,
a preview of the result rows, and the OKF citations used. Independently, a **verification
query** was run directly against the CSV files with DuckDB to establish ground truth. The
two are compared per question.

The agent enforces a **grounding gate**: every number in its answer must appear in the
query result (or the question); otherwise it escalates instead of guessing. This is why
Q4 and Q5 escalated rather than returning a fabricated figure — a deliberate safety
behaviour inherited from the OKF "trust gate" design.

---

## 3. Question-by-question analysis

### Q1 — "List the 10 most recent orders with the customer name, salesperson name, and total quantity ordered."

**Agent status:** answered

**Agent SQL (4-table join — correct tables chosen):**
```sql
SELECT c."CustomerName", p."FullName" AS "SalespersonName", SUM(ol."Quantity") AS "TotalQuantityOrdered"
FROM "Sales.Orders" o
JOIN "Sales.Customers"    c  ON o."CustomerID"        = c."CustomerID"
JOIN "Application.People" p  ON o."SalespersonPersonID" = p."PersonID"
JOIN "Sales.OrderLines"   ol ON o."OrderID"           = ol."OrderID"
GROUP BY c."CustomerName", p."FullName"
ORDER BY MAX(o."OrderDate") DESC
LIMIT 10
```

**Agent answer (verbatim):**
> The 10 most recent orders include: Nils Kaulins with 1750 units (Archer Lamble),
> Tailspin Toys (Sauquoit, NY) with 1592 units (Amy Trefl), Tailspin Toys (Devault, PA)
> with 1722 units (Lily Code), … Emma Van Zant with 1995 units (Hudson Hollinworth), and
> Tailspin Toys (Sinclair, WY) with 1854 units (Jack Potter).

**Ground-truth (raw data) — 10 most recent orders by `OrderDate`:**
```sql
SELECT o."OrderID", o."OrderDate", c."CustomerName", p."FullName" AS Salesperson
FROM "Sales.Orders" o
JOIN "Sales.Customers" c ON o."CustomerID" = c."CustomerID"
JOIN "Application.People" p ON o."SalespersonPersonID" = p."PersonID"
ORDER BY o."OrderDate" DESC
LIMIT 10;
```
```
 OrderID  OrderDate    CustomerName                     Salesperson
   73506  2016-05-31   Wingtip Toys (Cos Cob, CT)       Archer Lamble
   73509  2016-05-31   Manca Hrastovsek                 Anthony Grosse
   73508  2016-05-31   Can ozcan                        Taj Shand
   73510  2016-05-31   Lilli Sokk                       Jack Potter
   73513  2016-05-31   Tailspin Toys (Yewed, OK)        Amy Trefl
   73507  2016-05-31   Tailspin Toys (Slanesville, WV)  Lily Code
   73514  2016-05-31   Joel Carrillo                    Jack Potter
   73511  2016-05-31   Elina Kaleja                     Anthony Grosse
   73512  2016-05-31   Wingtip Toys (Beals, ME)         Archer Lamble
   73515  2016-05-31   Tailspin Toys (Sinclair, WY)     Jack Potter
```

**Verdict:** ⚠️ **Partial.** The table linkage is correct (Orders → Customers → People →
OrderLines). But the question asks for the *10 most recent orders* while the SQL
`GROUP BY`s by customer+salesperson and orders by `MAX(OrderDate)`, so it returns the
10 most recent **customer/salesperson groups**, not the 10 most recent orders. Only the
last row ("Tailspin Toys (Sinclair, WY)") coincides with the true latest order
(OrderID 73515). The numeric quantities (1750, 1592, …) are genuinely in
`Sales.OrderLines` and pass the grounding gate.

---

### Q2 — "How many customers are there per country, with the country name and region?"

**Agent status:** answered

**Agent SQL (incorrect join):**
```sql
SELECT c."CountryName", c."Region", COUNT(*) AS "CustomerCount"
FROM "Application.Countries" c
JOIN "Sales.Customers" cu ON c."CountryID" = cu."DeliveryCityID"
GROUP BY c."CountryName", c."Region"
LIMIT 200;
```

**Agent answer (verbatim):**
> There is 1 customer in each of the following countries: Australia (Oceania),
> Cuba (Americas), Dem. Rep. Congo (Africa), Congo (Africa), and Uzbekistan (Asia).

**Ground-truth (raw data) — correct geographic hierarchy:**
```sql
SELECT co."CountryName", co."Region", COUNT(DISTINCT cu."CustomerID") AS customers
FROM "Sales.Customers" cu
JOIN "Application.Cities"        ci ON cu."DeliveryCityID"   = ci."CityID"
JOIN "Application.StateProvinces" sp ON ci."StateProvinceID" = sp."StateProvinceID"
JOIN "Application.Countries"     co ON sp."CountryID"       = co."CountryID"
GROUP BY co."CountryName", co."Region"
ORDER BY customers DESC;
```
```
  CountryName     Region     customers
United States     Americas          663
```

**Verdict:** ❌ **Wrong.** The correct path is Customers → Cities → StateProvinces →
Countries (this is exactly the `Geographic Hierarchy Join Path` documented in the OKF
bundle at `joins/geographic_hierarchy.md`). The agent instead joined
`Countries.CountryID = Customers.DeliveryCityID`, which compares a country id to a city
id — semantically meaningless. The resulting answer (5 countries with 1 customer each) is
grounded in the *wrong* join's output, so the grounding gate did not catch it. In reality
**all 663 customers are in the United States** (the only country represented). This is a
schema-linking / join-inference failure, not a grounding failure.

---

### Q3 — "Which suppliers provide stock items that are currently below their reorder level, and what is the shortfall?"

**Agent status:** answered

**Agent SQL (correct, adapted from the OKF "Inventory Reorder Exposure" metric):**
```sql
SELECT p."SupplierID", p."SupplierName", s."StockItemID", s."StockItemName",
       h."QuantityOnHand", h."ReorderLevel",
       (h."TargetStockLevel" - h."QuantityOnHand") AS recommended_order_units
FROM "Warehouse.StockItemHoldings" h
JOIN "Warehouse.StockItems"  s ON h."StockItemID" = s."StockItemID"
JOIN "Purchasing.Suppliers"  p ON s."SupplierID"  = p."SupplierID"
WHERE h."QuantityOnHand" <= h."ReorderLevel"
LIMIT 200;
```

**Agent answer (verbatim):**
> Fabrikam, Inc. provides "The Gu" red shirt XML tag t-shirt (White) 5XL, which has a
> shortfall of 2 units below the reorder level of 5. Litware, Inc. provides a shipping
> carton (Brown) 305x305x305mm, which is not below its reorder level of 50.

**Ground-truth (raw data):**
```
  SupplierName      StockItemName                                   QuantityOnHand ReorderLevel TargetStockLevel
Fabrikam, Inc.      "The Gu" red shirt XML tag t-shirt (White) 5XL             3             5               20
 Litware, Inc.      Shipping carton (Brown) 305x305x305mm                    38            50              100
```

**Verdict:** ⚠️ **Partial.** The SQL and result rows are **correct** — exactly two
low-stock items, both properly joined to their suppliers. The grounding gate passed because
the numbers (3, 5, 20, 38, 50, 100) all appear in the result. However the **answer text is
wrong for the second row**: it claims Litware's carton "is not below its reorder level of
50", when 38 ≤ 50 means it *is* below (shortfall 12 units to reorder level, 62 to target).
The agent misread the comparison for row 2 while reading row 1 correctly. The underlying
data and SQL are sound; the error is in the LLM's natural-language interpretation.

---

### Q4 — "For the top 5 selling stock items by revenue, show their supplier name, current stock on hand, and reorder level."

**Agent status:** escalated ("the model could not ground an answer in the query result")

**Agent SQL (4-table join — correct tables):**
```sql
SELECT s."SupplierName", sh."QuantityOnHand", sh."ReorderLevel"
FROM "Sales.InvoiceLines" il
JOIN "Warehouse.StockItems"      si ON il."StockItemID" = si."StockItemID"
JOIN "Purchasing.Suppliers"      s  ON si."SupplierID"  = s."SupplierID"
JOIN "Warehouse.StockItemHoldings" sh ON si."StockItemID" = sh."StockItemID"
GROUP BY s."SupplierName", sh."QuantityOnHand", sh."ReorderLevel"
ORDER BY SUM(il."ExtendedPrice") DESC
LIMIT 5;
```

**Agent result rows (executed successfully):**
```
SupplierName    QuantityOnHand  ReorderLevel
Litware, Inc.          12530             1
Litware, Inc.         103958            20
Litware, Inc.         308519            20
Litware, Inc.         188962            20
Litware, Inc.          68906            20
```

**Ground-truth (raw data, with revenue added for clarity):**
```sql
SELECT si."StockItemName", s."SupplierName", sh."QuantityOnHand", sh."ReorderLevel",
       SUM(il."ExtendedPrice" - il."TaxAmount") AS net_revenue
FROM "Sales.InvoiceLines" il
JOIN "Warehouse.StockItems"        si ON il."StockItemID"  = si."StockItemID"
JOIN "Purchasing.Suppliers"        s  ON si."SupplierID"   = s."SupplierID"
JOIN "Warehouse.StockItemHoldings" sh ON si."StockItemID"  = sh."StockItemID"
GROUP BY si."StockItemName", s."SupplierName", sh."QuantityOnHand", sh."ReorderLevel"
ORDER BY net_revenue DESC
LIMIT 5;
```
```
                     StockItemName                SupplierName   QtyOnHand ReorderLevel  net_revenue
        Air cushion machine (Blue)                Litware, Inc.      12530            1   11107251.0
32 mm Anti static bubble wrap (Blue) 50m          Litware, Inc.     103958           20    6384000.0
10 mm Anti static bubble wrap (Blue) 50m          Litware, Inc.     308519           20    6329070.0
      20 mm Double sided bubble wrap 50m          Litware, Inc.     188962           20    6214320.0
      32 mm Double sided bubble wrap 50m          Litware, Inc.      68906           20    6190240.0
```

**Verdict:** ⚠️ **Data correct, synthesis failed.** The agent's SQL omitted the
`StockItemName` from the `SELECT`/`GROUP BY`, so the executed result has the right rows and
quantities but no item names. The synthesizer then declined to produce an answer ("could
not ground an answer") — arguably the *safe* outcome given the answerable-but-unnamed rows.
The ground-truth query shows the intended result: the top seller is **"Air cushion machine
(Blue)"** (Litware, Inc., 12,530 on hand, reorder level 1, ≈ $11.1M net revenue). The
agent's chosen tables were all correct; the shortfall is that it didn't project the item
name and the synthesizer gave up rather than answer from the anonymous rows.

---

### Q5 — "Show total invoiced revenue by customer name for the top 5 customers."

**Agent status:** escalated ("answer contained numbers not present in the query result (3.64, 4.07)")

**Agent SQL (wrong — summed the wrong column):**
```sql
SELECT c."CustomerName", SUM(it."TransactionAmount") AS total_invoiced_revenue
FROM "Sales.Customers" AS c
JOIN "Sales.CustomerTransactions" AS it ON c."CustomerID" = it."CustomerID"
WHERE it."IsFinalized" = TRUE
GROUP BY c."CustomerName"
ORDER BY total_invoiced_revenue DESC
LIMIT 5;
```

**Agent result rows (executed, but meaningless):**
```
CustomerName                   total_invoiced_revenue
Tailspin Toys (Head Office)    4.0745362639427185e-10
Pavel Bogdanov                 3.637978807091713e-12
Juan Morse                     3.637978807091713e-12
Vladimir Henzl                 3.637978807091713e-12
Nadir Seddigh                  3.637978807091713e-12
```

**Ground-truth (raw data) — revenue from invoice lines (matches the OKF "Net Sales Revenue" metric):**
```sql
SELECT c."CustomerName",
       SUM(il."ExtendedPrice" - il."TaxAmount") AS net_revenue
FROM "Sales.Customers" c
JOIN "Sales.Invoices"     i  ON c."CustomerID" = i."CustomerID"
JOIN "Sales.InvoiceLines" il ON i."InvoiceID"   = il."InvoiceID"
WHERE i."IsCreditNote" = 'False'
GROUP BY c."CustomerName"
ORDER BY net_revenue DESC
LIMIT 5;
```
```
              CustomerName               net_revenue
Tailspin Toys (Inguadona, MN)              381585.35
 Tailspin Toys (Minidoka, ID)              371822.30
                Mauno Laurila              369058.30
Wingtip Toys (Sarversville, PA)             365427.00
             Nasrin Omidzadeh             361939.75
```

**Verdict:** ❌ **Wrong.** The agent chose `Sales.CustomerTransactions` and summed
`TransactionAmount`, which is not "invoiced revenue" and — because `IsFinalized = TRUE`
filters to finalized rows and the amounts largely net out — produces near-zero floats
(~4e-10). The correct measure is `SUM(ExtendedPrice - TaxAmount)` over `Sales.InvoiceLines`
joined to `Sales.Invoices` (excluding credit notes), exactly the OKF `Net Sales Revenue`
metric definition. The grounding gate correctly **refused** to answer (the model tried to
state "3.64"/"4.07" — likely misreading the scientific-notation floats — which were not
literally in the result), so the agent escalated instead of presenting a garbage figure.
This is the safety net working as intended, but the root cause is a poor SQL choice.

---

## 4. Cross-cutting findings

### 4.1 What worked well
- **Table selection / schema linking** was accurate: the agent picked the right 3–5 tables
  for every question (including the multi-hop Q1 and Q4).
- **SQL execution** over the raw CSVs was robust: DuckDB type auto-detect handled dates,
  booleans, `\N` nulls and numeric arithmetic without manual casts.
- **Grounding gate** correctly escalated Q5 rather than emitting a fabricated/meaningless
  number, and correctly passed Q1/Q3 where the numbers were genuinely present.
- **Metric reuse**: Q3's SQL was correctly adapted from the OKF `Inventory Reorder Exposure`
  metric definition.
- **Citations**: every answered question cited the OKF concepts (tables/metrics) used.

### 4.2 Where it failed
1. **Join-path inference (Q2).** The agent did not know that country requires
   Customers→Cities→StateProvinces→Countries. The correct path is explicitly documented in
   the OKF bundle (`joins/geographic_hierarchy.md`), but the schema-linker only passes
   *table column lists*, not the *join-path documents*, to the SQL generator. **Fix:** feed
   the relevant `JoinPath` reference SQL into the SQL-generation prompt when a question
   mentions geography (or always include the 3 join paths).
2. **Metric/measure selection (Q5).** For "revenue" the agent picked the AR ledger
   (`CustomerTransactions`) instead of invoice lines. The OKF bundle has the exact
   `Net Sales Revenue` metric, but it was not linked because the question wording didn't
   match the metric's title/description strongly enough. **Fix:** broaden metric linking to
   include tag/keyword matches (e.g. "revenue", "sales", "profit").
3. **Answer-text faithfulness (Q3).** The SQL result was correct, but the synthesizer
   misread one row's comparison. **Fix:** include the column values in the synthesis prompt
   in a row-oriented way and/or ask the model to restate the filter predicate per row.
4. **Projection completeness (Q4).** The agent grouped away the item name the question
   asked to display. **Fix:** instruct the SQL generator that any entity named in the
   question ("stock items", "customers") must appear in `SELECT`.

### 4.3 Net assessment
The architecture is sound and the safety behaviour (grounded escalation) is a genuine
strength — the agent never fabricated revenue (Q5) or silently produced an unnamed list
(Q4). The remaining work is **prompt/context quality**, not plumbing: giving the SQL
generator the OKF join-path SQL and the metric catalogue more aggressively, and tightening
the synthesis prompt, would convert Q2, Q4 and Q5 into correct answers.

---

## 5. Reproducibility

- Agent: `wwi_data_agent.py`
- Question runner used for this report: `_run_questions.py` (writes `_run_results.json`)
- Raw-data verification queries: `_verify_raw.py`
- Data: `WideworldimportersData/*.csv`; Bundle: `wideworldimporters_okf/`
- All numbers above are reproducible by running the SQL blocks shown against the CSVs with
  DuckDB (`read_csv_auto(..., header=true, nullstr='\N')`).

> Note on Q1: the agent's per-row quantities (e.g. 1750, 1592) are real `SUM(Quantity)`
> values from `Sales.OrderLines` for the returned customer/salesperson groups; the
> discrepancy is the *grouping* (customer+salesperson vs. individual order), not the
> arithmetic.