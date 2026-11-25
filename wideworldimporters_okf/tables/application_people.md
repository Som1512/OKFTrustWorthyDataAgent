---
type: Table
title: Application.People
description: Directory of employees, salespersons, system users, and external customer/supplier contacts.
resource: WideworldimportersData/Application.People.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 1111
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Directory of employees, salespersons, system users, and external customer/supplier contacts. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **1,111** rows and **21** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PersonID` | INT64 | Primary key identifier. |
| `FullName` | STRING | Attribute `FullName` of `Application.People`. |
| `PreferredName` | STRING | Attribute `PreferredName` of `Application.People`. |
| `SearchName` | STRING | Attribute `SearchName` of `Application.People`. |
| `IsPermittedToLogon` | BOOL | Attribute `IsPermittedToLogon` of `Application.People`. |
| `LogonName` | STRING | Attribute `LogonName` of `Application.People`. |
| `IsExternalLogonProvider` | BOOL | Attribute `IsExternalLogonProvider` of `Application.People`. |
| `HashedPassword` | STRING | Attribute `HashedPassword` of `Application.People`. |
| `IsSystemUser` | BOOL | Attribute `IsSystemUser` of `Application.People`. |
| `IsEmployee` | BOOL | Attribute `IsEmployee` of `Application.People`. |
| `IsSalesperson` | BOOL | Attribute `IsSalesperson` of `Application.People`. |
| `UserPreferences` | STRING | Attribute `UserPreferences` of `Application.People`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Application.People`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Application.People`. |
| `EmailAddress` | STRING | Attribute `EmailAddress` of `Application.People`. |
| `Photo` | STRING | Attribute `Photo` of `Application.People`. |
| `CustomFields` | STRING | Attribute `CustomFields` of `Application.People`. |
| `OtherLanguages` | STRING | Attribute `OtherLanguages` of `Application.People`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Historical row versions archived in [Application.People_Archive](/tables/application_people_archive.md) on `PersonID`.
