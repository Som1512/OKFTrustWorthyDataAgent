---
type: Table
title: Sales.CustomerCategories
description: Classification segments for customers (e.g., Supermarket, Novelty Shop, Gift Store).
resource: WideworldimportersData/Sales.CustomerCategories.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 8
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Classification segments for customers (e.g., Supermarket, Novelty Shop, Gift Store). Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **8** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CustomerCategoryID` | INT64 | Primary key identifier. |
| `CustomerCategoryName` | STRING | Attribute `CustomerCategoryName` of `Sales.CustomerCategories`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Sales.CustomerCategories_Archive](/tables/sales_customer_categories_archive.md) on `CustomerCategoryID`.
