---
type: Table
title: Application.DeliveryMethods
description: Lookup table defining shipping and freight delivery methods used for customer and supplier orders.
resource: WideworldimportersData/Application.DeliveryMethods.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 10
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Lookup table defining shipping and freight delivery methods used for customer and supplier orders. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **10** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `DeliveryMethodID` | INT64 | Primary key identifier. |
| `DeliveryMethodName` | STRING | Attribute `DeliveryMethodName` of `Application.DeliveryMethods`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.DeliveryMethods_Archive](/tables/application_delivery_methods_archive.md) on `DeliveryMethodID`.
