---
type: Metric
title: Gross Profit and Margin
description: Total line-level gross profit and gross profit margin percentage across invoiced sales.
resource: WideworldimportersData/Sales.InvoiceLines.csv
tags: [metric, sales, profitability, finance]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Gross Profit** captures the pre-tax profit generated on each invoiced line item (`LineProfit`), and **Gross Margin %** expresses that profit as a share of pre-tax net sales revenue.

# Calculation

```sql
SELECT
  SUM(il.LineProfit) AS total_gross_profit,
  SUM(il.LineProfit) / NULLIF(SUM(il.ExtendedPrice - il.TaxAmount), 0) AS gross_margin_pct
FROM Sales.InvoiceLines AS il
JOIN Sales.Invoices AS i
  ON il.InvoiceID = i.InvoiceID;
```

# Source Tables & Columns

- [Sales.InvoiceLines](/tables/sales_invoice_lines.md): `LineProfit`, `ExtendedPrice`, `TaxAmount`, `StockItemID`
- [Sales.Invoices](/tables/sales_invoices.md): `InvoiceID`, `InvoiceDate`, `SalespersonPersonID`
