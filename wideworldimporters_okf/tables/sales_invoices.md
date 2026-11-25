---
type: Table
title: Sales.Invoices
description: Header records for customer sales invoices and credit notes, tracking fulfillment, delivery confirmation, and dry/chiller counts.
resource: WideworldimportersData/Sales.Invoices.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 70510
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Header records for customer sales invoices and credit notes, tracking fulfillment, delivery confirmation, and dry/chiller counts. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **70,510** rows and **25** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `InvoiceID` | INT64 | Primary key identifier. |
| `CustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `BillToCustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `OrderID` | INT64 | Foreign key referencing `OrderID` in [Sales.Orders](/tables/sales_orders.md). |
| `DeliveryMethodID` | INT64 | Foreign key referencing `DeliveryMethodID` in [Application.DeliveryMethods](/tables/application_delivery_methods.md). |
| `ContactPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `AccountsPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `SalespersonPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `PackedByPersonID` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `InvoiceDate` | STRING | Attribute `InvoiceDate` of `Sales.Invoices`. |
| `CustomerPurchaseOrderNumber` | INT64 | Attribute `CustomerPurchaseOrderNumber` of `Sales.Invoices`. |
| `IsCreditNote` | BOOL | Attribute `IsCreditNote` of `Sales.Invoices`. |
| `CreditNoteReason` | STRING | Attribute `CreditNoteReason` of `Sales.Invoices`. |
| `Comments` | STRING | Attribute `Comments` of `Sales.Invoices`. |
| `DeliveryInstructions` | STRING | Attribute `DeliveryInstructions` of `Sales.Invoices`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Sales.Invoices`. |
| `TotalDryItems` | INT64 | Attribute `TotalDryItems` of `Sales.Invoices`. |
| `TotalChillerItems` | INT64 | Attribute `TotalChillerItems` of `Sales.Invoices`. |
| `DeliveryRun` | FLOAT64 | Attribute `DeliveryRun` of `Sales.Invoices`. |
| `RunPosition` | FLOAT64 | Attribute `RunPosition` of `Sales.Invoices`. |
| `ReturnedDeliveryData` | STRING | Attribute `ReturnedDeliveryData` of `Sales.Invoices`. |
| `ConfirmedDeliveryTime` | STRING | Attribute `ConfirmedDeliveryTime` of `Sales.Invoices`. |
| `ConfirmedReceivedBy` | STRING | Attribute `ConfirmedReceivedBy` of `Sales.Invoices`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Sales.Customers](/tables/sales_customers.md) on `BillToCustomerID = CustomerID`.
- Joined with [Sales.Orders](/tables/sales_orders.md) on `OrderID`.
- Joined with [Application.DeliveryMethods](/tables/application_delivery_methods.md) on `DeliveryMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `ContactPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `AccountsPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `SalespersonPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `PackedByPersonID = PersonID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
