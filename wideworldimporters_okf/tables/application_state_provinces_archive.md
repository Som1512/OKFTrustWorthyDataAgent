---
type: Table
title: Application.StateProvinces_Archive
description: System-versioned temporal archive preserving historical versions of state/province records.
resource: WideworldimportersData/Application.StateProvinces_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 104
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of state/province records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **104** rows and **10** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StateProvinceID` | INT64 | Identifier referencing `StateProvinceID` in [Application.StateProvinces](/tables/application_state_provinces.md). |
| `StateProvinceCode` | STRING | Attribute `StateProvinceCode` of `Application.StateProvinces_Archive`. |
| `StateProvinceName` | STRING | Attribute `StateProvinceName` of `Application.StateProvinces_Archive`. |
| `CountryID` | INT64 | Foreign key referencing `CountryID` in [Application.Countries](/tables/application_countries.md). |
| `SalesTerritory` | STRING | Attribute `SalesTerritory` of `Application.StateProvinces_Archive`. |
| `Border` | STRING | Attribute `Border` of `Application.StateProvinces_Archive`. |
| `LatestRecordedPopulation` | INT64 | Attribute `LatestRecordedPopulation` of `Application.StateProvinces_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.StateProvinces](/tables/application_state_provinces.md) on `StateProvinceID`.
- Joined with [Application.Countries](/tables/application_countries.md) on `CountryID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
