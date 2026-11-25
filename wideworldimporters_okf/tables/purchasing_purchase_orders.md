---
type: Table
title: Purchasing.PurchaseOrders
description: Header records for purchase orders placed with external suppliers, including expected delivery and finalization status.
resource: WideworldimportersData/Purchasing.PurchaseOrders.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 2074
tags: [wideworldimporters, purchasing, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Header records for purchase orders placed with external suppliers, including expected delivery and finalization status. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **2,074** rows and **12** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `PurchaseOrderID` | INT64 | Primary key identifier. |
| `SupplierID` | INT64 | Foreign key referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `OrderDate` | STRING | Attribute `OrderDate` of `Purchasing.PurchaseOrders`. |
| `DeliveryMethodID` | INT64 | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `ContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ExpectedDeliveryDate` | STRING | Attribute `ExpectedDeliveryDate` of `Purchasing.PurchaseOrders`. |
| `SupplierReference` | STRING | Attribute `SupplierReference` of `Purchasing.PurchaseOrders`. |
| `IsOrderFinalized` | BOOL | Attribute `IsOrderFinalized` of `Purchasing.PurchaseOrders`. |
| `Comments` | STRING | Attribute `Comments` of `Purchasing.PurchaseOrders`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Purchasing.PurchaseOrders`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `ContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
