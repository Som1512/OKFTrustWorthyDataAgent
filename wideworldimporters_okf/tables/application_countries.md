---
type: Table
title: Application.Countries
description: Reference table of sovereign nations and territories including ISO codes, regions, population, and geographic borders.
resource: WideworldimportersData/Application.Countries.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 190
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Reference table of sovereign nations and territories including ISO codes, regions, population, and geographic borders. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **190** rows and **14** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CountryID` | INT64 | Primary key identifier. |
| `CountryName` | STRING | Attribute `CountryName` of `Application.Countries`. |
| `FormalName` | STRING | Attribute `FormalName` of `Application.Countries`. |
| `IsoAlpha3Code` | STRING | Attribute `IsoAlpha3Code` of `Application.Countries`. |
| `IsoNumericCode` | INT64 | Attribute `IsoNumericCode` of `Application.Countries`. |
| `CountryType` | STRING | Attribute `CountryType` of `Application.Countries`. |
| `LatestRecordedPopulation` | INT64 | Attribute `LatestRecordedPopulation` of `Application.Countries`. |
| `Continent` | STRING | Attribute `Continent` of `Application.Countries`. |
| `Region` | STRING | Attribute `Region` of `Application.Countries`. |
| `Subregion` | STRING | Attribute `Subregion` of `Application.Countries`. |
| `Border` | STRING | Attribute `Border` of `Application.Countries`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Application.Countries_Archive](/tables/application_countries_archive.md) on `CountryID`.
