---
type: Metric
title: Order Pick & Fill Rate
description: Ratio of picked item quantities to ordered item quantities across customer sales orders.
resource: WideworldimportersData/Sales.OrderLines.csv
tags: [metric, sales, fulfillment, warehouse]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Order Pick & Fill Rate** measures warehouse fulfillment accuracy and stock availability by comparing `PickedQuantity` against `Quantity` on [Sales.OrderLines](/tables/sales_order_lines.md).

# Calculation

```sql
SELECT
  SUM(ol.PickedQuantity) * 1.0 / NULLIF(SUM(ol.Quantity), 0) AS unit_fill_rate,
  COUNT(CASE WHEN ol.PickedQuantity >= ol.Quantity THEN 1 END) * 1.0 / COUNT(*) AS line_fill_rate
FROM Sales.OrderLines AS ol
JOIN Sales.Orders AS o
  ON ol.OrderID = o.OrderID;
```

# Source Tables & Columns

- [Sales.OrderLines](/tables/sales_order_lines.md): `Quantity`, `PickedQuantity`, `PickingCompletedWhen`, `OrderID`
- [Sales.Orders](/tables/sales_orders.md): `OrderID`, `OrderDate`, `IsUndersupplyBackordered`, `BackorderOrderID`
