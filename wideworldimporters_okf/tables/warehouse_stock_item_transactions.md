---
type: Table
title: Warehouse.StockItemTransactions
description: Inventory movement ledger tracking stock receipts, customer shipments, and stock adjustments.
resource: WideworldimportersData/Warehouse.StockItemTransactions.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 236667
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Inventory movement ledger tracking stock receipts, customer shipments, and stock adjustments. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **236,667** rows and **11** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockItemTransactionID` | INT64 | Primary key identifier. |
| `StockItemID` | INT64 | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `TransactionTypeID` | INT64 | Foreign key referencing `TransactionTypeID` in [Application.TransactionTypes](/tables/application_transaction_types.md). |
| `CustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `InvoiceID` | INT64 | Foreign key referencing `InvoiceID` in [Sales.Invoices](/tables/sales_invoices.md). |
| `SupplierID` | STRING | Foreign key referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `PurchaseOrderID` | STRING | Foreign key referencing `PurchaseOrderID` in [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md). |
| `TransactionOccurredWhen` | STRING | Attribute `TransactionOccurredWhen` of `Warehouse.StockItemTransactions`. |
| `Quantity` | FLOAT64 | Attribute `Quantity` of `Warehouse.StockItemTransactions`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Application.TransactionTypes](/tables/application_transaction_types.md) on `TransactionTypeID`.
- Joined with [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Sales.Invoices](/tables/sales_invoices.md) on `InvoiceID`.
- Joined with [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) on `PurchaseOrderID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
