---
type: Table
title: Application.TransactionTypes_Archive
description: System-versioned temporal archive preserving historical versions of transaction types.
resource: WideworldimportersData/Application.TransactionTypes_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 1
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of transaction types. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **1** rows and **5** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `TransactionTypeID` | INT64 | Identifier referencing `TransactionTypeID` in [Application.TransactionTypes](/tables/application_transaction_types.md). |
| `TransactionTypeName` | STRING | Attribute `TransactionTypeName` of `Application.TransactionTypes_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.TransactionTypes](/tables/application_transaction_types.md) on `TransactionTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
