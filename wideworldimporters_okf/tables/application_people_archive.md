---
type: Table
title: Application.People_Archive
description: System-versioned temporal archive preserving historical changes to people and user records.
resource: WideworldimportersData/Application.People_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 961
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical changes to people and user records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **961** rows and **21** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PersonID` | INT64 | Identifier referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `FullName` | STRING | Attribute `FullName` of `Application.People_Archive`. |
| `PreferredName` | STRING | Attribute `PreferredName` of `Application.People_Archive`. |
| `SearchName` | STRING | Attribute `SearchName` of `Application.People_Archive`. |
| `IsPermittedToLogon` | BOOL | Attribute `IsPermittedToLogon` of `Application.People_Archive`. |
| `LogonName` | STRING | Attribute `LogonName` of `Application.People_Archive`. |
| `IsExternalLogonProvider` | BOOL | Attribute `IsExternalLogonProvider` of `Application.People_Archive`. |
| `HashedPassword` | STRING | Attribute `HashedPassword` of `Application.People_Archive`. |
| `IsSystemUser` | BOOL | Attribute `IsSystemUser` of `Application.People_Archive`. |
| `IsEmployee` | BOOL | Attribute `IsEmployee` of `Application.People_Archive`. |
| `IsSalesperson` | BOOL | Attribute `IsSalesperson` of `Application.People_Archive`. |
| `UserPreferences` | STRING | Attribute `UserPreferences` of `Application.People_Archive`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Application.People_Archive`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Application.People_Archive`. |
| `EmailAddress` | STRING | Attribute `EmailAddress` of `Application.People_Archive`. |
| `Photo` | STRING | Attribute `Photo` of `Application.People_Archive`. |
| `CustomFields` | STRING | Attribute `CustomFields` of `Application.People_Archive`. |
| `OtherLanguages` | STRING | Attribute `OtherLanguages` of `Application.People_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.People](/tables/application_people.md) on `PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
