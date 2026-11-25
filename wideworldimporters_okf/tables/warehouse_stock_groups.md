---
type: Table
title: Warehouse.StockGroups
description: Product catalog categories/groups used for merchandising and promotional targeting.
resource: WideworldimportersData/Warehouse.StockGroups.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 10
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Product catalog categories/groups used for merchandising and promotional targeting. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **10** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockGroupID` | INT64 | Primary key identifier. |
| `StockGroupName` | STRING | Attribute `StockGroupName` of `Warehouse.StockGroups`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Warehouse.StockGroups_Archive](/tables/warehouse_stock_groups_archive.md) on `StockGroupID`.
