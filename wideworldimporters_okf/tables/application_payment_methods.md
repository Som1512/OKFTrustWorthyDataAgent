---
type: Table
title: Application.PaymentMethods
description: Lookup table defining accepted payment methods for customer receipts and supplier disbursements.
resource: WideworldimportersData/Application.PaymentMethods.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 4
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Lookup table defining accepted payment methods for customer receipts and supplier disbursements. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **4** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PaymentMethodID` | INT64 | Primary key identifier. |
| `PaymentMethodName` | STRING | Attribute `PaymentMethodName` of `Application.PaymentMethods`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.PaymentMethods_Archive](/tables/application_payment_methods_archive.md) on `PaymentMethodID`.
