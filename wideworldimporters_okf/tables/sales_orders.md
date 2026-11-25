---
type: Table
title: Sales.Orders
description: Header records for incoming customer sales orders, backorder links, picking timestamps, and delivery instructions.
resource: WideworldimportersData/Sales.Orders.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 73595
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Header records for incoming customer sales orders, backorder links, picking timestamps, and delivery instructions. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **73,595** rows and **16** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `OrderID` | INT64 | Primary key identifier. |
| `CustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `SalespersonPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `PickedByPersonID` | STRING | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `BackorderOrderID` | INT64 | Foreign key referencing `OrderID` in [Sales.Orders](/tables/sales_orders.md). |
| `OrderDate` | STRING | Attribute `OrderDate` of `Sales.Orders`. |
| `ExpectedDeliveryDate` | STRING | Attribute `ExpectedDeliveryDate` of `Sales.Orders`. |
| `CustomerPurchaseOrderNumber` | INT64 | Attribute `CustomerPurchaseOrderNumber` of `Sales.Orders`. |
| `IsUndersupplyBackordered` | BOOL | Attribute `IsUndersupplyBackordered` of `Sales.Orders`. |
| `Comments` | STRING | Attribute `Comments` of `Sales.Orders`. |
| `DeliveryInstructions` | STRING | Attribute `DeliveryInstructions` of `Sales.Orders`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Sales.Orders`. |
| `PickingCompletedWhen` | STRING | Attribute `PickingCompletedWhen` of `Sales.Orders`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Application.People](/tables/application_people.md) on `SalespersonPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `PickedByPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `ContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
