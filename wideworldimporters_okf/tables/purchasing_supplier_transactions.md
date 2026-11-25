---
type: Table
title: Purchasing.SupplierTransactions
description: Financial ledger entries recording supplier invoices, payments, credits, and outstanding balances.
resource: WideworldimportersData/Purchasing.SupplierTransactions.csv
dataset: /datasets/wideworldimporters.md
schema: purchasing
row_count: 2438
tags: [wideworldimporters, purchasing, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Financial ledger entries recording supplier invoices, payments, credits, and outstanding balances. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`purchasing` schema), containing **2,438** rows and **15** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SupplierTransactionID` | INT64 | Primary key identifier. |
| `SupplierID` | INT64 | Foreign key referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `TransactionTypeID` | INT64 | Foreign key referencing `TransactionTypeID` in [Application.TransactionTypes](/tables/application_transaction_types.md). |
| `PurchaseOrderID` | INT64 | Foreign key referencing `PurchaseOrderID` in [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md). |
| `PaymentMethodID` | INT64 | Foreign key referencing `PaymentMethodID` in [Application.PaymentMethods](/tables/application_payment_methods.md). |
| `SupplierInvoiceNumber` | INT64 | Attribute `SupplierInvoiceNumber` of `Purchasing.SupplierTransactions`. |
| `TransactionDate` | STRING | Attribute `TransactionDate` of `Purchasing.SupplierTransactions`. |
| `AmountExcludingTax` | FLOAT64 | Attribute `AmountExcludingTax` of `Purchasing.SupplierTransactions`. |
| `TaxAmount` | FLOAT64 | Attribute `TaxAmount` of `Purchasing.SupplierTransactions`. |
| `TransactionAmount` | FLOAT64 | Attribute `TransactionAmount` of `Purchasing.SupplierTransactions`. |
| `OutstandingBalance` | FLOAT64 | Attribute `OutstandingBalance` of `Purchasing.SupplierTransactions`. |
| `FinalizationDate` | STRING | Attribute `FinalizationDate` of `Purchasing.SupplierTransactions`. |
| `IsFinalized` | BOOL | Attribute `IsFinalized` of `Purchasing.SupplierTransactions`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Application.TransactionTypes](/tables/application_transaction_types.md) on `TransactionTypeID`.
- Joined with [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) on `PurchaseOrderID`.
- Joined with [Application.PaymentMethods](/tables/application_payment_methods.md) on `PaymentMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
