---
type: Table
title: Purchasing.Suppliers_Archive
description: System-versioned temporal archive preserving historical versions of supplier master records.
resource: WideworldimportersData/Purchasing.Suppliers_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 13
tags: [wideworldimporters, purchasing, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of supplier master records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **13** rows and **29** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SupplierID` | INT64 | Identifier referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `SupplierName` | STRING | Attribute `SupplierName` of `Purchasing.Suppliers_Archive`. |
| `SupplierCategoryID` | INT64 | Foreign key referencing `SupplierCategoryID` in [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md). |
| `PrimaryContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `AlternateContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `DeliveryMethodID` | STRING | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `DeliveryCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `PostalCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `SupplierReference` | STRING | Attribute `SupplierReference` of `Purchasing.Suppliers_Archive`. |
| `BankAccountName` | STRING | Attribute `BankAccountName` of `Purchasing.Suppliers_Archive`. |
| `BankAccountBranch` | STRING | Attribute `BankAccountBranch` of `Purchasing.Suppliers_Archive`. |
| `BankAccountCode` | INT64 | Attribute `BankAccountCode` of `Purchasing.Suppliers_Archive`. |
| `BankAccountNumber` | INT64 | Attribute `BankAccountNumber` of `Purchasing.Suppliers_Archive`. |
| `BankInternationalCode` | INT64 | Attribute `BankInternationalCode` of `Purchasing.Suppliers_Archive`. |
| `PaymentDays` | INT64 | Attribute `PaymentDays` of `Purchasing.Suppliers_Archive`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Purchasing.Suppliers_Archive`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Purchasing.Suppliers_Archive`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Purchasing.Suppliers_Archive`. |
| `WebsiteURL` | STRING | Attribute `WebsiteURL` of `Purchasing.Suppliers_Archive`. |
| `DeliveryAddressLine1` | STRING | Attribute `DeliveryAddressLine1` of `Purchasing.Suppliers_Archive`. |
| `DeliveryAddressLine2` | STRING | Attribute `DeliveryAddressLine2` of `Purchasing.Suppliers_Archive`. |
| `DeliveryPostalCode` | INT64 | Attribute `DeliveryPostalCode` of `Purchasing.Suppliers_Archive`. |
| `DeliveryLocation` | STRING | Attribute `DeliveryLocation` of `Purchasing.Suppliers_Archive`. |
| `PostalAddressLine1` | STRING | Attribute `PostalAddressLine1` of `Purchasing.Suppliers_Archive`. |
| `PostalAddressLine2` | STRING | Attribute `PostalAddressLine2` of `Purchasing.Suppliers_Archive`. |
| `PostalPostalCode` | INT64 | Attribute `PostalPostalCode` of `Purchasing.Suppliers_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md) on `SupplierCategoryID`.
- Joined with [Application.People](/tables/application_people.md) on `PrimaryContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `AlternateContactPersonID = PersonID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `DeliveryCityID = CityID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `PostalCityID = CityID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
