---
type: Table
title: Application.StateProvinces
description: Reference table of states, provinces, and territories mapped to countries and sales territories.
resource: WideworldimportersData/Application.StateProvinces.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 53
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Reference table of states, provinces, and territories mapped to countries and sales territories. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **53** rows and **10** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StateProvinceID` | INT64 | Primary key identifier. |
| `StateProvinceCode` | STRING | Attribute `StateProvinceCode` of `Application.StateProvinces`. |
| `StateProvinceName` | STRING | Attribute `StateProvinceName` of `Application.StateProvinces`. |
| `CountryID` | INT64 | Foreign key referencing `CountryID` in [Application.Countries](/tables/application_countries.md). |
| `SalesTerritory` | STRING | Attribute `SalesTerritory` of `Application.StateProvinces`. |
| `Border` | STRING | Attribute `Border` of `Application.StateProvinces`. |
| `LatestRecordedPopulation` | INT64 | Attribute `LatestRecordedPopulation` of `Application.StateProvinces`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.Countries](/tables/application_countries.md) on `CountryID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.StateProvinces_Archive](/tables/application_state_provinces_archive.md) on `StateProvinceID`.
