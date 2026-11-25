---
type: Table
title: Sales.BuyingGroups_Archive
description: System-versioned temporal archive preserving historical versions of buying groups.
resource: WideworldimportersData/Sales.BuyingGroups_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 0
tags: [wideworldimporters, sales, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of buying groups. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **0** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `BuyingGroupID` | STRING | Identifier referencing `BuyingGroupID` in [Sales.BuyingGroups](/tables/sales_buying_groups.md). |
| `BuyingGroupName` | STRING | Attribute `BuyingGroupName` of `Sales.BuyingGroups_Archive`. |
| `LastEditedBy` | STRING | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Sales.BuyingGroups](/tables/sales_buying_groups.md) on `BuyingGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
