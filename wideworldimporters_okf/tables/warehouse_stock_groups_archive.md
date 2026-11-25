---
type: Table
title: Warehouse.StockGroups_Archive
description: System-versioned temporal archive preserving historical versions of stock groups.
resource: WideworldimportersData/Warehouse.StockGroups_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 1
tags: [wideworldimporters, warehouse, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of stock groups. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockGroupID` | INT64 | Identifier referencing `StockGroupID` in [Warehouse.StockGroups](/tables/warehouse_stock_groups.md). |
| `StockGroupName` | STRING | Attribute `StockGroupName` of `Warehouse.StockGroups_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Warehouse.StockGroups](/tables/warehouse_stock_groups.md) on `StockGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
