---
type: Table
title: Application.Cities
description: Reference table of cities across states/provinces with spatial coordinates and recorded population.
resource: WideworldimportersData/Application.Cities.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 37940
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Reference table of cities across states/provinces with spatial coordinates and recorded population. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **37,940** rows and **8** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CityID` | INT64 | Primary key identifier. |
| `CityName` | STRING | Attribute `CityName` of `Application.Cities`. |
| `StateProvinceID` | INT64 | Foreign key referencing `StateProvinceID` in [Application.StateProvinces](/tables/application_state_provinces.md). |
| `Location` | STRING | Attribute `Location` of `Application.Cities`. |
| `LatestRecordedPopulation` | INT64 | Attribute `LatestRecordedPopulation` of `Application.Cities`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.StateProvinces](/tables/application_state_provinces.md) on `StateProvinceID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.Cities_Archive](/tables/application_cities_archive.md) on `CityID`.
