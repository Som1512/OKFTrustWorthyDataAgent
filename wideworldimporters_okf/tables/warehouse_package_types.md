---
type: Table
title: Warehouse.PackageTypes
description: Lookup table of unit and outer packaging types (e.g., Each, Carton, Box, Packet).
resource: WideworldimportersData/Warehouse.PackageTypes.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 14
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Lookup table of unit and outer packaging types (e.g., Each, Carton, Box, Packet). Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **14** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PackageTypeID` | INT64 | Primary key identifier. |
| `PackageTypeName` | STRING | Attribute `PackageTypeName` of `Warehouse.PackageTypes`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Warehouse.PackageTypes_Archive](/tables/warehouse_package_types_archive.md) on `PackageTypeID`.
