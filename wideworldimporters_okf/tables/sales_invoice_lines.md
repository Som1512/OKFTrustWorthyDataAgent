---
type: Table
title: Sales.InvoiceLines
description: Granular line items for customer invoices including quantities, unit prices, tax amounts, extended prices, and line profit.
resource: WideworldimportersData/Sales.InvoiceLines.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 228265
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Granular line items for customer invoices including quantities, unit prices, tax amounts, extended prices, and line profit. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **228,265** rows and **13** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `InvoiceLineID` | INT64 | Primary key identifier. |
| `InvoiceID` | INT64 | Foreign key referencing `InvoiceID` in [Sales.Invoices](/tables/sales_invoices.md). |
| `StockItemID` | INT64 | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `Description` | STRING | Attribute `Description` of `Sales.InvoiceLines`. |
| `PackageTypeID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `Quantity` | INT64 | Attribute `Quantity` of `Sales.InvoiceLines`. |
| `UnitPrice` | FLOAT64 | Attribute `UnitPrice` of `Sales.InvoiceLines`. |
| `TaxRate` | FLOAT64 | Attribute `TaxRate` of `Sales.InvoiceLines`. |
| `TaxAmount` | FLOAT64 | Attribute `TaxAmount` of `Sales.InvoiceLines`. |
| `LineProfit` | FLOAT64 | Attribute `LineProfit` of `Sales.InvoiceLines`. |
| `ExtendedPrice` | FLOAT64 | Attribute `ExtendedPrice` of `Sales.InvoiceLines`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Sales.Invoices](/tables/sales_invoices.md) on `InvoiceID`.
- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
