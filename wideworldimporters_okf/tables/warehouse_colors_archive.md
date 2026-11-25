---
type: Table
title: Warehouse.Colors_Archive
description: System-versioned temporal archive preserving historical versions of product colors.
resource: WideworldimportersData/Warehouse.Colors_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 1
tags: [wideworldimporters, warehouse, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of product colors. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `ColorID` | INT64 | Identifier referencing `ColorID` in [Warehouse.Colors](/tables/warehouse_colors.md). |
| `ColorName` | STRING | Attribute `ColorName` of `Warehouse.Colors_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Warehouse.Colors](/tables/warehouse_colors.md) on `ColorID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
