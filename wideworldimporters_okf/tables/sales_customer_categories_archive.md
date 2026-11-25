---
type: Table
title: Sales.CustomerCategories_Archive
description: System-versioned temporal archive preserving historical versions of customer categories.
resource: WideworldimportersData/Sales.CustomerCategories_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 1
tags: [wideworldimporters, sales, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of customer categories. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CustomerCategoryID` | INT64 | Identifier referencing `CustomerCategoryID` in [Sales.CustomerCategories](/tables/sales_customer_categories.md). |
| `CustomerCategoryName` | STRING | Attribute `CustomerCategoryName` of `Sales.CustomerCategories_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Sales.CustomerCategories](/tables/sales_customer_categories.md) on `CustomerCategoryID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
