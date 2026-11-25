---
type: Table
title: Warehouse.StockItemStockGroups
description: Many-to-many junction table mapping stock items to one or more product stock groups.
resource: WideworldimportersData/Warehouse.StockItemStockGroups.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 442
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Many-to-many junction table mapping stock items to one or more product stock groups. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **442** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockItemStockGroupID` | INT64 | Primary key identifier. |
| `StockItemID` | INT64 | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `StockGroupID` | INT64 | Foreign key referencing `StockGroupID` in [Warehouse.StockGroups](/tables/warehouse_stock_groups.md). |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Warehouse.StockGroups](/tables/warehouse_stock_groups.md) on `StockGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
