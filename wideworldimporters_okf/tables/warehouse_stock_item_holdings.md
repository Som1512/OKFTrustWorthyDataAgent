---
type: Table
title: Warehouse.StockItemHoldings
description: Current inventory levels, bin locations, last cost price, reorder thresholds, and target stock levels per item.
resource: WideworldimportersData/Warehouse.StockItemHoldings.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 227
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Current inventory levels, bin locations, last cost price, reorder thresholds, and target stock levels per item. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **227** rows and **9** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockItemID` | INT64 | Primary key identifier. |
| `QuantityOnHand` | INT64 | Attribute `QuantityOnHand` of `Warehouse.StockItemHoldings`. |
| `BinLocation` | STRING | Attribute `BinLocation` of `Warehouse.StockItemHoldings`. |
| `LastStocktakeQuantity` | INT64 | Attribute `LastStocktakeQuantity` of `Warehouse.StockItemHoldings`. |
| `LastCostPrice` | FLOAT64 | Attribute `LastCostPrice` of `Warehouse.StockItemHoldings`. |
| `ReorderLevel` | INT64 | Attribute `ReorderLevel` of `Warehouse.StockItemHoldings`. |
| `TargetStockLevel` | INT64 | Attribute `TargetStockLevel` of `Warehouse.StockItemHoldings`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
