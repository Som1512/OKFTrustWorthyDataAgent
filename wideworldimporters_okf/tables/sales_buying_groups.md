---
type: Table
title: Sales.BuyingGroups
description: Corporate retail chains or buying groups that aggregate multiple customer accounts.
resource: WideworldimportersData/Sales.BuyingGroups.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 2
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Corporate retail chains or buying groups that aggregate multiple customer accounts. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **2** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `BuyingGroupID` | INT64 | Primary key identifier. |
| `BuyingGroupName` | STRING | Attribute `BuyingGroupName` of `Sales.BuyingGroups`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Sales.BuyingGroups_Archive](/tables/sales_buying_groups_archive.md) on `BuyingGroupID`.
