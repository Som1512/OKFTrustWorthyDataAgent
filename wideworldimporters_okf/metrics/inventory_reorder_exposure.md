---
type: Metric
title: Inventory Reorder Exposure
description: Count and replenishment gap of stock items whose QuantityOnHand has fallen at or below ReorderLevel.
resource: WideworldimportersData/Warehouse.StockItemHoldings.csv
tags: [metric, warehouse, inventory, purchasing]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Inventory Reorder Exposure** identifies SKUs in [Warehouse.StockItemHoldings](/tables/warehouse_stock_item_holdings.md) requiring supplier replenishment and computes the unit shortfall relative to `TargetStockLevel`.

# Calculation

```sql
SELECT
  h.StockItemID,
  s.StockItemName,
  h.QuantityOnHand,
  h.ReorderLevel,
  h.TargetStockLevel,
  (h.TargetStockLevel - h.QuantityOnHand) AS recommended_order_units
FROM Warehouse.StockItemHoldings AS h
JOIN Warehouse.StockItems AS s
  ON h.StockItemID = s.StockItemID
WHERE h.QuantityOnHand <= h.ReorderLevel;
```

# Source Tables & Columns

- [Warehouse.StockItemHoldings](/tables/warehouse_stock_item_holdings.md): `StockItemID`, `QuantityOnHand`, `ReorderLevel`, `TargetStockLevel`, `LastCostPrice`
- [Warehouse.StockItems](/tables/warehouse_stock_items.md): `StockItemID`, `StockItemName`, `SupplierID`, `LeadTimeDays`
