---
type: JoinPath
title: Geographic Hierarchy Join Path
description: Canonical snowflake dimension join path linking customers and suppliers to cities, states/provinces, and countries.
resource: WideworldimportersData/Application.Cities.csv
tags: [joins, application, geography, dimensions]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Resolves delivery and postal city identifiers on [Sales.Customers](/tables/sales_customers.md) and [Purchasing.Suppliers](/tables/purchasing_suppliers.md) up through state/province sales territories and countries.

# Join Graph

1. [Sales.Customers](/tables/sales_customers.md) (`DeliveryCityID`) → [Application.Cities](/tables/application_cities.md) (`CityID`)
2. [Purchasing.Suppliers](/tables/purchasing_suppliers.md) (`DeliveryCityID`) → [Application.Cities](/tables/application_cities.md) (`CityID`)
3. [Application.Cities](/tables/application_cities.md) (`StateProvinceID`) → [Application.StateProvinces](/tables/application_state_provinces.md) (`StateProvinceID`)
4. [Application.StateProvinces](/tables/application_state_provinces.md) (`CountryID`) → [Application.Countries](/tables/application_countries.md) (`CountryID`)
