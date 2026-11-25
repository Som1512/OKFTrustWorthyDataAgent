---
type: Table
title: Sales.Customers
description: Master directory of B2B customers including billing relationships, credit limits, payment days, and delivery runs.
resource: WideworldimportersData/Sales.Customers.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 663
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Master directory of B2B customers including billing relationships, credit limits, payment days, and delivery runs. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **663** rows and **31** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CustomerID` | INT64 | Primary key identifier. |
| `CustomerName` | STRING | Attribute `CustomerName` of `Sales.Customers`. |
| `BillToCustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `CustomerCategoryID` | INT64 | Foreign key referencing `CustomerCategoryID` in [Sales.CustomerCategories](/tables/sales_customer_categories.md). |
| `BuyingGroupID` | INT64 | Foreign key referencing `BuyingGroupID` in [Sales.BuyingGroups](/tables/sales_buying_groups.md). |
| `PrimaryContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `AlternateContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `DeliveryMethodID` | INT64 | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `DeliveryCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `PostalCityID` | INT64 | Foreign key referencing `CityID` in [Application.Cities](/tables/application_cities.md). |
| `CreditLimit` | STRING | Attribute `CreditLimit` of `Sales.Customers`. |
| `AccountOpenedDate` | STRING | Attribute `AccountOpenedDate` of `Sales.Customers`. |
| `StandardDiscountPercentage` | FLOAT64 | Attribute `StandardDiscountPercentage` of `Sales.Customers`. |
| `IsStatementSent` | BOOL | Attribute `IsStatementSent` of `Sales.Customers`. |
| `IsOnCreditHold` | BOOL | Attribute `IsOnCreditHold` of `Sales.Customers`. |
| `PaymentDays` | INT64 | Attribute `PaymentDays` of `Sales.Customers`. |
| `PhoneNumber` | STRING | Attribute `PhoneNumber` of `Sales.Customers`. |
| `FaxNumber` | STRING | Attribute `FaxNumber` of `Sales.Customers`. |
| `DeliveryRun` | FLOAT64 | Attribute `DeliveryRun` of `Sales.Customers`. |
| `RunPosition` | FLOAT64 | Attribute `RunPosition` of `Sales.Customers`. |
| `WebsiteURL` | STRING | Attribute `WebsiteURL` of `Sales.Customers`. |
| `DeliveryAddressLine1` | STRING | Attribute `DeliveryAddressLine1` of `Sales.Customers`. |
| `DeliveryAddressLine2` | STRING | Attribute `DeliveryAddressLine2` of `Sales.Customers`. |
| `DeliveryPostalCode` | INT64 | Attribute `DeliveryPostalCode` of `Sales.Customers`. |
| `DeliveryLocation` | STRING | Attribute `DeliveryLocation` of `Sales.Customers`. |
| `PostalAddressLine1` | STRING | Attribute `PostalAddressLine1` of `Sales.Customers`. |
| `PostalAddressLine2` | STRING | Attribute `PostalAddressLine2` of `Sales.Customers`. |
| `PostalPostalCode` | INT64 | Attribute `PostalPostalCode` of `Sales.Customers`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Sales.CustomerCategories](/tables/sales_customer_categories.md) on `CustomerCategoryID`.
- Joined with [Sales.BuyingGroups](/tables/sales_buying_groups.md) on `BuyingGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `PrimaryContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `AlternateContactPersonID = PersonID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `DeliveryCityID = CityID`.
- Joined with [Application.Cities](/tables/application_cities.md) on `PostalCityID = CityID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Sales.Customers_Archive](/tables/sales_customers_archive.md) on `CustomerID`.
