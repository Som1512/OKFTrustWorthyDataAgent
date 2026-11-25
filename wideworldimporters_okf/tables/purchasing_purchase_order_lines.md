---
type: Table
title: Purchasing.PurchaseOrderLines
description: Line-item details for supplier purchase orders, tracking ordered/received outer packages and expected unit prices.
resource: WideworldimportersData/Purchasing.PurchaseOrderLines.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 8367
tags: [wideworldimporters, purchasing, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Line-item details for supplier purchase orders, tracking ordered/received outer packages and expected unit prices. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **8,367** rows and **12** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PurchaseOrderLineID` | INT64 | Primary key identifier. |
| `PurchaseOrderID` | INT64 | Foreign key referencing `PurchaseOrderID` in [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md). |
| `StockItemID` | INT64 | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `OrderedOuters` | INT64 | Attribute `OrderedOuters` of `Purchasing.PurchaseOrderLines`. |
| `Description` | STRING | Attribute `Description` of `Purchasing.PurchaseOrderLines`. |
| `ReceivedOuters` | INT64 | Attribute `ReceivedOuters` of `Purchasing.PurchaseOrderLines`. |
| `PackageTypeID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `ExpectedUnitPricePerOuter` | FLOAT64 | Attribute `ExpectedUnitPricePerOuter` of `Purchasing.PurchaseOrderLines`. |
| `LastReceiptDate` | STRING | Attribute `LastReceiptDate` of `Purchasing.PurchaseOrderLines`. |
| `IsOrderLineFinalized` | BOOL | Attribute `IsOrderLineFinalized` of `Purchasing.PurchaseOrderLines`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) on `PurchaseOrderID`.
- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
