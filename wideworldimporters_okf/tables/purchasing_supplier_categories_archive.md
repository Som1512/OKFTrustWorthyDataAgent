---
type: Table
title: Purchasing.SupplierCategories_Archive
description: System-versioned temporal archive preserving historical versions of supplier categories.
resource: WideworldimportersData/Purchasing.SupplierCategories_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 1
tags: [wideworldimporters, purchasing, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of supplier categories. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SupplierCategoryID` | INT64 | Identifier referencing `SupplierCategoryID` in [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md). |
| `SupplierCategoryName` | STRING | Attribute `SupplierCategoryName` of `Purchasing.SupplierCategories_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md) on `SupplierCategoryID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
