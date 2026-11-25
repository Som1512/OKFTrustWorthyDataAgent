---
type: Table
title: Purchasing.Suppliers
description: Master directory of vendors and suppliers including banking details, payment terms, contacts, and addresses.
resource: WideworldimportersData/Purchasing.Suppliers.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 13
tags: [wideworldimporters, purchasing, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Master directory of vendors and suppliers including banking details, payment terms, contacts, and addresses. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **13** rows and **29** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SupplierID` | INT64 | Primary key identifier. |
| `SupplierName` | STRING | Attribute `SupplierName` of `Purchasing.Suppliers`. |
| `SupplierCategoryID` | INT64 | Foreign key referencing `SupplierCategoryID` in [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md). |
| `PrimaryContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `AlternateContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `DeliveryMethodID` | STRING | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `DeliveryCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `PostalCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `SupplierReference` | STRING | Attribute `SupplierReference` of `Purchasing.Suppliers`. |
| `BankAccountName` | STRING | Attribute `BankAccountName` of `Purchasing.Suppliers`. |
| `BankAccountBranch` | STRING | Attribute `BankAccountBranch` of `Purchasing.Suppliers`. |
| `BankAccountCode` | INT64 | Attribute `BankAccountCode` of `Purchasing.Suppliers`. |
| `BankAccountNumber` | INT64 | Attribute `BankAccountNumber` of `Purchasing.Suppliers`. |
| `BankInternationalCode` | INT64 | Attribute `BankInternationalCode` of `Purchasing.Suppliers`. |
| `PaymentDays` | INT64 | Attribute `PaymentDays` of `Purchasing.Suppliers`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Purchasing.Suppliers`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Purchasing.Suppliers`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Purchasing.Suppliers`. |
| `WebsiteURL` | STRING | Attribute `WebsiteURL` of `Purchasing.Suppliers`. |
| `DeliveryAddressLine1` | STRING | Attribute `DeliveryAddressLine1` of `Purchasing.Suppliers`. |
| `DeliveryAddressLine2` | STRING | Attribute `DeliveryAddressLine2` of `Purchasing.Suppliers`. |
| `DeliveryPostalCode` | INT64 | Attribute `DeliveryPostalCode` of `Purchasing.Suppliers`. |
| `DeliveryLocation` | STRING | Attribute `DeliveryLocation` of `Purchasing.Suppliers`. |
| `PostalAddressLine1` | STRING | Attribute `PostalAddressLine1` of `Purchasing.Suppliers`. |
| `PostalAddressLine2` | STRING | Attribute `PostalAddressLine2` of `Purchasing.Suppliers`. |
| `PostalPostalCode` | INT64 | Attribute `PostalPostalCode` of `Purchasing.Suppliers`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md) on `SupplierCategoryID`.
- Joined with [Application.People](/tables/application_people.md) on `PrimaryContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `AlternateContactPersonID = PersonID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `DeliveryCityID = CityID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `PostalCityID = CityID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Purchasing.Suppliers_Archive](/tables/purchasing_suppliers_archive.md) on `SupplierID`.
