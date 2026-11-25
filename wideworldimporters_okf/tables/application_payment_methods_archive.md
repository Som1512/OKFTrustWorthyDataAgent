---
type: Table
title: Application.PaymentMethods_Archive
description: System-versioned temporal archive preserving historical versions of payment methods.
resource: WideworldimportersData/Application.PaymentMethods_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 1
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of payment methods. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PaymentMethodID` | INT64 | Identifier referencing `PaymentMethodID` in [Application.PaymentMethods](/tables/application_payment_methods.md). |
| `PaymentMethodName` | STRING | Attribute `PaymentMethodName` of `Application.PaymentMethods_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.PaymentMethods](/tables/application_payment_methods.md) on `PaymentMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
