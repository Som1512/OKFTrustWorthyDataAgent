---
type: Table
title: Application.TransactionTypes
description: Lookup table categorizing financial and inventory transaction types across ledger and stock movements.
resource: WideworldimportersData/Application.TransactionTypes.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 13
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Lookup table categorizing financial and inventory transaction types across ledger and stock movements. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **13** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `TransactionTypeID` | INT64 | Primary key identifier. |
| `TransactionTypeName` | STRING | Attribute `TransactionTypeName` of `Application.TransactionTypes`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.TransactionTypes_Archive](/tables/application_transaction_types_archive.md) on `TransactionTypeID`.
