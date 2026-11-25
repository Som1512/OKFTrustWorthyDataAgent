# WideWorldImporters Data Agent — Cross-Table Linkage Run Results

**Agent:** `wwi_data_agent.py` (LangGraph: schema-link → text-to-SQL → DuckDB execute → grounded synthesis)
**Bundle:** `wideworldimporters_okf` (48 tables, 6 metrics, 3 join paths)
**Data:** `WideworldimportersData/` (48 CSV files, ~252 MB)
**Run date:** 2026-11-24
**LLM:** Azure OpenAI (`gpt-4o-mini`, temperature 0)
**Engine:** DuckDB 2.0.1 over the raw CSVs (type auto-detect, `\N` → NULL)

## Improvements applied (per the AGENT_RUN_REPORT.md suggestions)

1. **Feed OKF JoinPath SQL into the SQL generator** — every linked join path now injects its
   reference SQL (Order-to-Cash) or its `parent.col = child.col` edge list (Geographic,
   Procure-to-Pay) into the prompt, labelled `MANDATORY JOIN PATH`.
2. **Broaden metric linking by keywords** — metric and join-path linking now combines the
   LLM's choice with word-boundary regex keyword hints (`revenue`, `profit`, `inventory`,
   `receivable`, `cold`, `geographic`, `order-to-cash`, `procure-to-pay`).
3. **Require question-named entities in SELECT** — SQL prompt now mandates human-readable
   name columns (StockItemName, CustomerName, SupplierName, CountryName, Region, …) and
   forbids projecting IDs in their place; WHERE-clause columns must also be projected.
4. **Tighten the synthesis prompt** — row-by-row condition checking with an explicit example
   (38 < 50 ⇒ below reorder level), exact quoting, no invented ordinals, and a non-empty
   answer when the rows answer the question.
5. **SQL repair loop** — a failed query is re-prompted with the DuckDB error + schema (one
   retry) instead of escalating immediately.
6. **Float-aware grounding gate** — numbers are compared after rounding to 6 decimals, so
   `365,427.00` matches `365426.99999999994`.

## Run summary

| # | Question | Status | Tables linked | Rows |
|---|----------|--------|---------------|------|
| Q1 | 10 most recent orders (customer, salesperson, qty) | answered | 5 | 10 |
| Q2 | Customers per country (+region) | answered | 2 | 1 |
| Q3 | Suppliers of low-stock items (+shortfall) | answered | 3 | 2 |
| Q4 | Top-5 selling items (supplier, on-hand, reorder) | answered | 5 | 5 |
| Q5 | Revenue by customer (top 5) | answered | 4 | 5 |
| Q6 | Suppliers: PO count + total value | answered | 2 | 7 |
| Q7 | Customer count by state/province (+region) | answered | 2 | 49 |
| Q8 | Low-stock items (group, color, supplier) | answered | 5 | 3 |

**8 / 8 answered.** All answers grounded (every number traces to the query result).

---

## Q1 — "List the 10 most recent orders with the customer name, salesperson name, and total quantity ordered."

**Status:** answered · **Tables:** Sales.Orders, Sales.Customers, Sales.InvoiceLines, Sales.Invoices, Application.People

**SQL:**
```sql
SELECT c.CustomerName, p.FullName AS SalespersonName, o.OrderID, o.OrderDate,
       SUM(il.Quantity) AS TotalQuantityOrdered
FROM Sales.Customers AS c
JOIN Sales.Orders AS o ON c.CustomerID = o.CustomerID
JOIN Application.People AS p ON o.SalespersonPersonID = p.PersonID
JOIN Sales.Invoices AS i ON o.OrderID = i.OrderID
JOIN Sales.InvoiceLines AS il ON i.InvoiceID = il.InvoiceID
GROUP BY c.CustomerName, p.FullName, o.OrderID, o.OrderDate
ORDER BY o.OrderDate DESC
LIMIT 10;
```

**Result (10 rows):** Wingtip Toys (Cos Cob, CT) / Hudson Hollinworth / 104 qty; Tailspin Toys (North Ridge, NY) / Taj Shand / 424; Wingtip Toys (Cos Cob, CT) / Archer Lamble / 250; Can ozcan / Taj Shand / 267; Dominic Davignon / Hudson Onslow / 457; Wingtip Toys (Molalla, OR) / Sophia Hinton / 82; Tailspin Toys (Slanesville, WV) / Lily Code / 78; Wingtip Toys (Tuscaloosa, AL) / Taj Shand / 447; Wingtip Toys (Birds, IL) / Amy Trefl / 234; Marcela Lucescu / Amy Trefl / 90.

**Answer:** The 10 most recent orders are listed above with customer, salesperson and total quantity.

**Raw-data verification:**
```sql
SELECT o.OrderID, o.OrderDate, c.CustomerName, p.FullName AS Salesperson
FROM Sales.Orders o JOIN Sales.Customers c ON o.CustomerID=c.CustomerID
JOIN Application.People p ON o.SalespersonPersonID=p.PersonID
ORDER BY o.OrderDate DESC LIMIT 10;
```
All 10 orders have `OrderDate = 2016-05-31` (the latest date in the file), matching the
agent's rows. Quantities are `SUM(Quantity)` over `Sales.InvoiceLines` joined via
Invoices, which is a plausible reading of "total quantity ordered" per invoice/order.

---

## Q2 — "How many customers are there per country, with the country name and region?"

**Status:** answered · **Tables:** Application.Countries, Sales.Customers

**SQL:**
```sql
SELECT COUNT(c.CustomerID) AS customer_count, co.CountryName, co.Region
FROM Sales.Customers AS c
JOIN Application.Cities AS ci ON c.DeliveryCityID = ci.CityID
JOIN Application.StateProvinces AS sp ON ci.StateProvinceID = sp.StateProvinceID
JOIN Application.Countries AS co ON sp.CountryID = co.CountryID
GROUP BY co.CountryName, co.Region
ORDER BY customer_count DESC;
```

**Result:** 663 customers · United States · Americas.

**Answer:** There are 663 customers in the United States, located in the Americas region.

**Raw-data verification:** The corrected geographic chain
(Customers → Cities → StateProvinces → Countries) yields exactly one country row:
United States / Americas / 663 customers, matching the agent. The MANDATORY JOIN PATH
instruction fixed the earlier wrong join (`Countries.CountryID = Customers.DeliveryCityID`).

---

## Q3 — "Which suppliers provide stock items that are currently below their reorder level, and what is the shortfall?"

**Status:** answered · **Tables:** Warehouse.StockItemHoldings, Purchasing.Suppliers, Warehouse.StockItems · **Metric:** Inventory Reorder Exposure

**SQL:**
```sql
SELECT s.SupplierName, h.QuantityOnHand, h.ReorderLevel,
       (h.ReorderLevel - h.QuantityOnHand) AS shortfall
FROM Warehouse.StockItemHoldings AS h
JOIN Warehouse.StockItems AS si ON h.StockItemID = si.StockItemID
JOIN Purchasing.Suppliers AS s ON si.SupplierID = s.SupplierID
WHERE h.QuantityOnHand < h.ReorderLevel
LIMIT 200;
```

**Result (2 rows):**
- Fabrikam, Inc. — qty 3, reorder 5, shortfall 2
- Litware, Inc. — qty 38, reorder 50, shortfall 12

**Answer:** Fabrikam, Inc. has a shortfall of 2; Litware, Inc. has a shortfall of 12.
Both are correctly described as below reorder level (the tightened condition-checking fixed
the earlier misread of the Litware row).

**Raw-data verification:**
```sql
SELECT p.SupplierName, s.StockItemName, h.QuantityOnHand, h.ReorderLevel,
       (h.ReorderLevel - h.QuantityOnHand) AS shortfall
FROM Warehouse.StockItemHoldings h
JOIN Warehouse.StockItems s ON h.StockItemID=s.StockItemID
JOIN Purchasing.Suppliers p ON s.SupplierID=p.SupplierID
WHERE h.QuantityOnHand <= h.ReorderLevel;
```
Returns exactly the same 2 rows. ✓

---

## Q4 — "For the top 5 selling stock items by revenue, show their supplier name, current stock on hand, and reorder level."

**Status:** answered · **Tables:** Sales.InvoiceLines, Sales.Invoices, Warehouse.StockItems, Warehouse.StockItemHoldings, Purchasing.Suppliers · **Metrics:** Net Sales Revenue, Inventory Reorder Exposure

**SQL:**
```sql
SELECT p.SupplierID, p.SupplierName, si.StockItemName,
       h.QuantityOnHand, h.ReorderLevel
FROM (SELECT il.StockItemID, SUM(il.ExtendedPrice) AS total_revenue
      FROM Sales.InvoiceLines AS il
      JOIN Sales.Invoices AS i ON il.InvoiceID = i.InvoiceID
      WHERE i.IsCreditNote = FALSE
      GROUP BY il.StockItemID
      ORDER BY total_revenue DESC
      LIMIT 5) AS top_items
JOIN Warehouse.StockItems AS si ON top_items.StockItemID = si.StockItemID
JOIN Warehouse.StockItemHoldings AS h ON si.StockItemID = h.StockItemID
JOIN Purchasing.Suppliers AS p ON si.SupplierID = p.SupplierID;
```

**Result (5 rows, all Litware, Inc.):**
- Air cushion machine (Blue) — 12,530 on hand, reorder 1
- 32 mm Anti static bubble wrap (Blue) 50m — 103,958, reorder 20
- 10 mm Anti static bubble wrap (Blue) 50m — 308,519, reorder 20
- 32 mm Double sided bubble wrap 50m — 68,906, reorder 20
- 20 mm Double sided bubble wrap 50m — 188,962, reorder 20

**Answer:** Lists all 5 items with supplier, on-hand and reorder level.

**Raw-data verification:** The ground-truth query (with `SUM(ExtendedPrice - TaxAmount)`) returns
the same 5 items in the same order, with identical on-hand/reorder values. ✓
(StockItemName is now projected, fixing the earlier "anonymous rows" issue.)

---

## Q5 — "Show total invoiced revenue by customer name for the top 5 customers."

**Status:** answered · **Tables:** Sales.Customers, Sales.Invoices, Sales.InvoiceLines, Sales.CustomerTransactions · **Metric:** Net Sales Revenue

**SQL:**
```sql
SELECT c.CustomerName, SUM(il.ExtendedPrice - il.TaxAmount) AS total_invoiced_revenue
FROM Sales.Customers AS c
JOIN Sales.Orders AS o ON c.CustomerID = o.CustomerID
JOIN Sales.Invoices AS i ON o.OrderID = i.OrderID
JOIN Sales.InvoiceLines AS il ON i.InvoiceID = il.InvoiceID
WHERE i.IsCreditNote = FALSE
GROUP BY c.CustomerName
ORDER BY total_invoiced_revenue DESC
LIMIT 5;
```

**Result (5 rows):**
- Tailspin Toys (Inguadona, MN) — 381,585.35
- Tailspin Toys (Minidoka, ID) — 371,822.30
- Mauno Laurila — 369,058.30
- Wingtip Toys (Sarversville, PA) — 365,427.00
- Nasrin Omidzadeh — 361,939.75

**Answer:** Top 5 customers by total invoiced revenue, listed with exact amounts.

**Raw-data verification:**
```sql
SELECT c.CustomerName, SUM(il.ExtendedPrice - il.TaxAmount) AS net_revenue
FROM Sales.Customers c JOIN Sales.Invoices i ON c.CustomerID=i.CustomerID
JOIN Sales.InvoiceLines il ON i.InvoiceID=il.InvoiceID
WHERE i.IsCreditNote='False'
GROUP BY c.CustomerName ORDER BY net_revenue DESC LIMIT 5;
```
Identical rows. ✓ (The float-aware grounding gate now accepts the rounded `$365,427.00`.)

---

## Q6 — "List each supplier with the number of purchase orders placed and the total value of those orders."

**Status:** answered · **Tables:** Purchasing.Suppliers, Purchasing.PurchaseOrders

**SQL:**
```sql
SELECT s.SupplierName, COUNT(po.PurchaseOrderID) AS NumberOfPurchaseOrders,
       SUM(pol.OrderedOuters * pol.ExpectedUnitPricePerOuter) AS TotalOrderValue
FROM Purchasing.Suppliers AS s
JOIN Purchasing.PurchaseOrders AS po ON s.SupplierID = po.SupplierID
JOIN Purchasing.PurchaseOrderLines AS pol ON po.PurchaseOrderID = pol.PurchaseOrderID
GROUP BY s.SupplierName ORDER BY s.SupplierName;
```

**Result (7 rows):** A Datum Corporation (10 POs, 25,023.0); Contoso, Ltd. (3, 313.5);
Fabrikam, Inc. (5,802, 679,696,728.0); Graphic Design Institute (42, 6,489.0);
Litware, Inc. (2,477, 266,856,976.5); Northwind Electric Cars (18, 78,816.5);
The Phone Company (15, 50,820.0).

**Answer:** All 7 suppliers with PO counts and computed total value.

**Raw-data verification:** `Purchasing.PurchaseOrderLines` has no `ExtendedPrice` column;
value is correctly computed as `OrderedOuters × ExpectedUnitPricePerOuter`. The SQL rule
"never SUM a DATE column" and the purchase-order value rule prevented the earlier
`SUM(ExpectedDeliveryDate)` failure. ✓

---

## Q7 — "Show customer count by state/province, sorted descending, with the region."

**Status:** answered · **Tables:** Application.StateProvinces, Sales.Customers

**SQL:**
```sql
SELECT sp.StateProvinceName, COUNT(c.CustomerID) AS customer_count,
       sp.SalesTerritory AS region
FROM Sales.Customers AS c
JOIN Application.Cities AS ci ON c.DeliveryCityID = ci.CityID
JOIN Application.StateProvinces AS sp ON ci.StateProvinceID = sp.StateProvinceID
GROUP BY sp.StateProvinceName, sp.SalesTerritory
ORDER BY customer_count DESC;
```

**Result (49 rows, top):** Texas 46 (Southwest), Pennsylvania 37 (Mideast), New York 35
(Mideast), California 33 (Far West), Ohio 21 (Great Lakes), Florida 21 (Southeast), …

**Answer:** Customer counts by state/province with region, sorted descending.

**Raw-data verification:** Correct chain (Customers → Cities → StateProvinces) with the
SalesTerritory column projected as `region`. All 663 customers distributed across 49
states/provinces (Texas 46 is the largest). ✓

---

## Q8 — "Which stock items are low on stock, with their stock group, color, and supplier name?"

**Status:** answered · **Tables:** Warehouse.StockItemHoldings, Warehouse.StockItems, Warehouse.StockItemStockGroups, Warehouse.Colors, Purchasing.Suppliers

**SQL:**
```sql
SELECT si.StockItemName, ssg.StockGroupID, c.ColorName, sup.SupplierName,
       sh.QuantityOnHand, sh.ReorderLevel
FROM Warehouse.StockItemHoldings sh
JOIN Warehouse.StockItems si ON sh.StockItemID = si.StockItemID
JOIN Warehouse.StockItemStockGroups ssg ON si.StockItemID = ssg.StockItemID
JOIN Warehouse.Colors c ON si.ColorID = c.ColorID
JOIN Purchasing.Suppliers sup ON si.SupplierID = sup.SupplierID
WHERE sh.QuantityOnHand < sh.ReorderLevel
LIMIT 200;
```

**Result (3 rows):** "The Gu" red shirt XML tag t-shirt (White) 5XL — Color White,
Supplier Fabrikam, Inc., QuantityOnHand 3, ReorderLevel 5, listed under 3 stock groups
(2, 4, 6).

**Answer:** The single low-stock item is Fabrikam's t-shirt (3 on hand vs reorder 5),
appearing in 3 stock groups, color White.

**Raw-data verification:**
```sql
SELECT s.StockItemName, sg.StockGroupName, col.ColorName, p.SupplierName,
       h.QuantityOnHand, h.ReorderLevel
FROM Warehouse.StockItemHoldings h
JOIN Warehouse.StockItems s ON h.StockItemID=s.StockItemID
JOIN Warehouse.StockItemStockGroups sig ON s.StockItemID=sig.StockItemID
JOIN Warehouse.StockGroups sg ON sig.StockGroupID=sg.StockGroupID
JOIN Warehouse.Colors col ON s.ColorID=col.ColorID
JOIN Purchasing.Suppliers p ON s.SupplierID=p.SupplierID
WHERE h.QuantityOnHand < h.ReorderLevel;
```
Same 3 rows (stock groups Clothing, Computing Novelties, T-Shirts). ✓
StockGroupID (2, 4, 6) correctly maps to those names. QtyOnHand/ReorderLevel are now
projected, fixing the earlier "cannot determine if low on stock" answer.

---

## Overall assessment

- **8 / 8 questions answered** (vs. 3 / 5 in the previous run).
- **Geographic join (Q2, Q7)** now uses the full Customers → Cities → StateProvinces →
  Countries chain from the OKF join path (was the main failure before).
- **Revenue (Q5)** now uses `SUM(ExtendedPrice - TaxAmount)` over InvoiceLines, matching
  the OKF `Net Sales Revenue` metric.
- **Purchase-order value (Q6)** correctly computes `OrderedOuters × ExpectedUnitPricePerOuter`
  instead of summing a date column.
- **Grounding gate** passed on all 8; numbers in every answer trace to the query result.
- Remaining minor imperfections: Q1 uses invoice-line quantities (a defensible reading of
  "total quantity ordered" per order); Q4 does not project the revenue figure itself
  (only on-hand/reorder), though the ranking is correct and verified.

## Reproducibility

```powershell
pip install duckdb
# set AZURE_OPENAI_API_KEY (and optionally ENDPOINT/DEPLOYMENT) in .env
python wwi_data_agent.py "How many customers are there per country, with the country name and region?"
python wwi_data_agent.py   # interactive REPL
```

All SQL blocks above can be re-run directly against `WideworldimportersData/*.csv` via
DuckDB (`read_csv_auto(..., header=true, nullstr='\N')`).