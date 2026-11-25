---
type: Table
title: Warehouse.Colors
description: Lookup table of standard product colors assigned to stock items.
resource: WideworldimportersData/Warehouse.Colors.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 36
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Lookup table of standard product colors assigned to stock items. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **36** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `ColorID` | INT64 | Primary key identifier. |
| `ColorName` | STRING | Attribute `ColorName` of `Warehouse.Colors`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Warehouse.Colors_Archive](/tables/warehouse_colors_archive.md) on `ColorID`.
