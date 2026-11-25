---
type: Table
title: Application.SystemParameters
description: Global application configuration, corporate headquarters addresses, and system settings.
resource: WideworldimportersData/Application.SystemParameters.csv
dataset: /datasets/wideworldimporters.md
schema: application
row_count: 148
tags: [wideworldimporters, application, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Global application configuration, corporate headquarters addresses, and system settings. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`application` schema), containing **148** rows and **13** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SystemParameterID` | INT64 | Primary key identifier. |
| `DeliveryAddressLine1` | STRING | Attribute `DeliveryAddressLine1` of `Application.SystemParameters`. |
| `DeliveryAddressLine2` | STRING | Attribute `DeliveryAddressLine2` of `Application.SystemParameters`. |
| `DeliveryCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `DeliveryPostalCode` | INT64 | Attribute `DeliveryPostalCode` of `Application.SystemParameters`. |
| `DeliveryLocation` | STRING | Attribute `DeliveryLocation` of `Application.SystemParameters`. |
| `PostalAddressLine1` | STRING | Attribute `PostalAddressLine1` of `Application.SystemParameters`. |
| `PostalAddressLine2` | STRING | Attribute `PostalAddressLine2` of `Application.SystemParameters`. |
| `PostalCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `PostalPostalCode` | INT64 | Attribute `PostalPostalCode` of `Application.SystemParameters`. |
| `ApplicationSettings` | STRING | Attribute `ApplicationSettings` of `Application.SystemParameters`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Application.Cities](/tables/application_cities.md) on `DeliveryCityID = CityID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `PostalCityID = CityID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
