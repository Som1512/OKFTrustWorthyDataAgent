---
type: Table
title: Sales.Customers_Archive
description: System-versioned temporal archive preserving historical versions of customer master records.
resource: WideworldimportersData/Sales.Customers_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 51
tags: [wideworldimporters, sales, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of customer master records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **51** rows and **31** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CustomerID` | INT64 | Identifier referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `CustomerName` | STRING | Attribute `CustomerName` of `Sales.Customers_Archive`. |
| `BillToCustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `CustomerCategoryID` | INT64 | Foreign key referencing `CustomerCategoryID` in [Sales.CustomerCategories](/tables/sales_customer_categories.md). |
| `BuyingGroupID` | STRING | Foreign key referencing `BuyingGroupID` in [Sales.BuyingGroups](/tables/sales_buying_groups.md). |
| `PrimaryContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `AlternateContactPersonID` | STRING | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `DeliveryMethodID` | INT64 | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `DeliveryCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `PostalCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `CreditLimit` | FLOAT64 | Attribute `CreditLimit` of `Sales.Customers_Archive`. |
| `AccountOpenedDate` | STRING | Attribute `AccountOpenedDate` of `Sales.Customers_Archive`. |
| `StandardDiscountPercentage` | FLOAT64 | Attribute `StandardDiscountPercentage` of `Sales.Customers_Archive`. |
| `IsStatementSent` | BOOL | Attribute `IsStatementSent` of `Sales.Customers_Archive`. |
| `IsOnCreditHold` | BOOL | Attribute `IsOnCreditHold` of `Sales.Customers_Archive`. |
| `PaymentDays` | INT64 | Attribute `PaymentDays` of `Sales.Customers_Archive`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Sales.Customers_Archive`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Sales.Customers_Archive`. |
| `DeliveryRun` | FLOAT64 | Attribute `DeliveryRun` of `Sales.Customers_Archive`. |
| `RunPosition` | FLOAT64 | Attribute `RunPosition` of `Sales.Customers_Archive`. |
| `WebsiteURL` | STRING | Attribute `WebsiteURL` of `Sales.Customers_Archive`. |
| `DeliveryAddressLine1` | STRING | Attribute `DeliveryAddressLine1` of `Sales.Customers_Archive`. |
| `DeliveryAddressLine2` | STRING | Attribute `DeliveryAddressLine2` of `Sales.Customers_Archive`. |
| `DeliveryPostalCode` | INT64 | Attribute `DeliveryPostalCode` of `Sales.Customers_Archive`. |
| `DeliveryLocation` | STRING | Attribute `DeliveryLocation` of `Sales.Customers_Archive`. |
| `PostalAddressLine1` | STRING | Attribute `PostalAddressLine1` of `Sales.Customers_Archive`. |
| `PostalAddressLine2` | STRING | Attribute `PostalAddressLine2` of `Sales.Customers_Archive`. |
| `PostalPostalCode` | INT64 | Attribute `PostalPostalCode` of `Sales.Customers_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Sales.Customers](/tables/sales_customers.md) on `BillToCustomerID = CustomerID`.
- Joined with [Sales.CustomerCategories](/tables/sales_customer_categories.md) on `CustomerCategoryID`.
- Joined with [Sales.BuyingGroups](/tables/sales_buying_groups.md) on `BuyingGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `PrimaryContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `AlternateContactPersonID = PersonID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `DeliveryCityID = CityID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `PostalCityID = CityID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
