---
type: Table
title: Application.Countries_Archive
description: System-versioned temporal archive preserving historical versions of country records.
resource: WideworldimportersData/Application.Countries_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 37
tags: [wideworldimporters, application, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of country records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **37** rows and **14** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CountryID` | INT64 | Identifier referencing `CountryID` in [Application.Countries](/tables/application_countries.md). |
| `CountryName` | STRING | Attribute `CountryName` of `Application.Countries_Archive`. |
| `FormalName` | STRING | Attribute `FormalName` of `Application.Countries_Archive`. |
| `IsoAlpha3Code` | STRING | Attribute `IsoAlpha3Code` of `Application.Countries_Archive`. |
| `IsoNumericCode` | INT64 | Attribute `IsoNumericCode` of `Application.Countries_Archive`. |
| `CountryType` | STRING | Attribute `CountryType` of `Application.Countries_Archive`. |
| `LatestRecordedPopulation` | INT64 | Attribute `LatestRecordedPopulation` of `Application.Countries_Archive`. |
| `Continent` | STRING | Attribute `Continent` of `Application.Countries_Archive`. |
| `Region` | STRING | Attribute `Region` of `Application.Countries_Archive`. |
| `Subregion` | STRING | Attribute `Subregion` of `Application.Countries_Archive`. |
| `Border` | STRING | Attribute `Border` of `Application.Countries_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Application.Countries](/tables/application_countries.md) on `CountryID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
