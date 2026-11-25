---
type: Table
title: Sales.OrderLines
description: Line-item details for customer sales orders including ordered quantities, picked quantities, and unit pricing.
resource: WideworldimportersData/Sales.OrderLines.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 231412
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Line-item details for customer sales orders including ordered quantities, picked quantities, and unit pricing. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **231,412** rows and **12** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `OrderLineID` | INT64 | Primary key identifier. |
| `OrderID` | INT64 | Foreign key referencing `OrderID` in [Sales.Orders](/tables/sales_orders.md). |
| `StockItemID` | INT64 | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `Description` | STRING | Attribute `Description` of `Sales.OrderLines`. |
| `PackageTypeID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `Quantity` | INT64 | Attribute `Quantity` of `Sales.OrderLines`. |
| `UnitPrice` | FLOAT64 | Attribute `UnitPrice` of `Sales.OrderLines`. |
| `TaxRate` | FLOAT64 | Attribute `TaxRate` of `Sales.OrderLines`. |
| `PickedQuantity` | INT64 | Attribute `PickedQuantity` of `Sales.OrderLines`. |
| `PickingCompletedWhen` | STRING | Attribute `PickingCompletedWhen` of `Sales.OrderLines`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Sales.Orders](/tables/sales_orders.md) on `OrderID`.
- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
