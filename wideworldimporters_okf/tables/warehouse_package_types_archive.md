---
type: Table
title: Warehouse.PackageTypes_Archive
description: System-versioned temporal archive preserving historical versions of package types.
resource: WideworldimportersData/Warehouse.PackageTypes_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 0
tags: [wideworldimporters, warehouse, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of package types. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **0** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PackageTypeID` | STRING | Identifier referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `PackageTypeName` | STRING | Attribute `PackageTypeName` of `Warehouse.PackageTypes_Archive`. |
| `LastEditedBy` | STRING | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
