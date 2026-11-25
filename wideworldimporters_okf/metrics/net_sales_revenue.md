---
type: Metric
title: Net Sales Revenue
description: Total invoiced revenue excluding sales tax across non-credit-note customer invoices.
resource: WideworldimportersData/Sales.InvoiceLines.csv
tags: [metric, sales, revenue, finance]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Net Sales Revenue** measures total recognized B2B wholesale revenue prior to sales tax, derived from [Sales.InvoiceLines](/tables/sales_invoice_lines.md) joined to [Sales.Invoices](/tables/sales_invoices.md).

# Calculation

```sql
SELECT
  SUM(il.ExtendedPrice - il.TaxAmount) AS net_sales_revenue
FROM Sales.InvoiceLines AS il
JOIN Sales.Invoices AS i
  ON il.InvoiceID = i.InvoiceID
WHERE i.IsCreditNote = FALSE;
```

# Source Tables & Columns

- [Sales.InvoiceLines](/tables/sales_invoice_lines.md): `ExtendedPrice`, `TaxAmount`, `InvoiceID`
- [Sales.Invoices](/tables/sales_invoices.md): `InvoiceID`, `InvoiceDate`, `IsCreditNote`, `CustomerID`
