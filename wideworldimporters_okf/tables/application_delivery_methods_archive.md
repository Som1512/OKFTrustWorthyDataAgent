---
type: Table
title: Application.DeliveryMethods_Archive
description: System-versioned temporal archive preserving historical versions of delivery methods.
resource: WideworldimportersData/Application.DeliveryMethods_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 1
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of delivery methods. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `DeliveryMethodID` | INT64 | Identifier referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `DeliveryMethodName` | STRING | Attribute `DeliveryMethodName` of `Application.DeliveryMethods_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
