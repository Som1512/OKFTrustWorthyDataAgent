---
type: Table
title: Purchasing.SupplierCategories
description: Classification categories for grouping suppliers (e.g., Novelty Goods Supplier, Packaging Supplier).
resource: WideworldimportersData/Purchasing.SupplierCategories.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 9
tags: [wideworldimporters, purchasing, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Classification categories for grouping suppliers (e.g., Novelty Goods Supplier, Packaging Supplier). Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **9** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SupplierCategoryID` | INT64 | Primary key identifier. |
| `SupplierCategoryName` | STRING | Attribute `SupplierCategoryName` of `Purchasing.SupplierCategories`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Purchasing.SupplierCategories_Archive](/tables/purchasing_supplier_categories_archive.md) on `SupplierCategoryID`.
