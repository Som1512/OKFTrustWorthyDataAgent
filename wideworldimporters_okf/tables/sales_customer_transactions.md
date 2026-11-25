---
type: Table
title: Sales.CustomerTransactions
description: Accounts receivable financial ledger recording customer invoices, payments, refunds, and balances.
resource: WideworldimportersData/Sales.CustomerTransactions.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 97147
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Accounts receivable financial ledger recording customer invoices, payments, refunds, and balances. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **97,147** rows and **14** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `CustomerTransactionID` | INT64 | Primary key identifier. |
| `CustomerID` | INT64 | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `TransactionTypeID` | INT64 | Foreign key referencing `TransactionTypeID` in [Application.TransactionTypes](/tables/application_transaction_types.md). |
| `InvoiceID` | INT64 | Foreign key referencing `InvoiceID` in [Sales.Invoices](/tables/sales_invoices.md). |
| `PaymentMethodID` | STRING | Foreign key referencing `PaymentMethodID` in [Application.PaymentMethods](/tables/application_payment_methods.md). |
| `TransactionDate` | STRING | Attribute `TransactionDate` of `Sales.CustomerTransactions`. |
| `AmountExcludingTax` | FLOAT64 | Attribute `AmountExcludingTax` of `Sales.CustomerTransactions`. |
| `TaxAmount` | FLOAT64 | Attribute `TaxAmount` of `Sales.CustomerTransactions`. |
| `TransactionAmount` | FLOAT64 | Attribute `TransactionAmount` of `Sales.CustomerTransactions`. |
| `OutstandingBalance` | FLOAT64 | Attribute `OutstandingBalance` of `Sales.CustomerTransactions`. |
| `FinalizationDate` | STRING | Attribute `FinalizationDate` of `Sales.CustomerTransactions`. |
| `IsFinalized` | BOOL | Attribute `IsFinalized` of `Sales.CustomerTransactions`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Application.TransactionTypes](/tables/application_transaction_types.md) on `TransactionTypeID`.
- Joined with [Sales.Invoices](/tables/sales_invoices.md) on `InvoiceID`.
- Joined with [Application.PaymentMethods](/tables/application_payment_methods.md) on `PaymentMethodID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
