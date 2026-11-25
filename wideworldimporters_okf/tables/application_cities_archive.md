---
type: Table
title: Application.Cities_Archive
description: System-versioned temporal archive preserving historical versions of city records.
resource: WideworldimportersData/Application.Cities_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 28
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of city records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **28** rows and **8** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CityID` | INT64 | Identifier referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `CityName` | STRING | Attribute `CityName` of `Application.Cities_Archive`. |
| `StateProvinceID` | INT64 | Foreign key referencing `StateProvinceID` in [Application.StateProvinces](/tables/application_state_provinces.md). |
| `Location` | STRING | Attribute `Location` of `Application.Cities_Archive`. |
| `LatestRecordedPopulation` | STRING | Attribute `LatestRecordedPopulation` of `Application.Cities_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.Cities](/tables/application_cities.md) on `CityID`.
- Joined with [Application.StateProvinces](/tables/application_state_provinces.md) on `StateProvinceID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
