---
type: JoinPath
title: Order-to-Cash Join Path
description: Canonical multi-table join path connecting customer master data, sales orders, invoices, and accounts receivable transactions.
resource: WideworldimportersData/Sales.Orders.csv
tags: [joins, sales, order-to-cash, finance]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Traces the end-to-end commercial lifecycle from customer account placement through order picking, invoicing, and payment settlement.

# Join Graph

1. [Sales.Customers](/tables/sales_customers.md) (`CustomerID`) → [Sales.Orders](/tables/sales_orders.md) (`CustomerID`)
2. [Sales.Orders](/tables/sales_orders.md) (`OrderID`) → [Sales.OrderLines](/tables/sales_order_lines.md) (`OrderID`)
3. [Sales.Orders](/tables/sales_orders.md) (`OrderID`) → [Sales.Invoices](/tables/sales_invoices.md) (`OrderID`)
4. [Sales.Invoices](/tables/sales_invoices.md) (`InvoiceID`) → [Sales.InvoiceLines](/tables/sales_invoice_lines.md) (`InvoiceID`)
5. [Sales.Invoices](/tables/sales_invoices.md) (`InvoiceID`) → [Sales.CustomerTransactions](/tables/sales_customer_transactions.md) (`InvoiceID`)
6. [Sales.InvoiceLines](/tables/sales_invoice_lines.md) (`StockItemID`) → [Warehouse.StockItems](/tables/warehouse_stock_items.md) (`StockItemID`)

# Reference SQL

```sql
SELECT
  c.CustomerName,
  o.OrderID,
  o.OrderDate,
  i.InvoiceID,
  i.InvoiceDate,
  si.StockItemName,
  il.Quantity,
  il.ExtendedPrice,
  il.LineProfit
FROM Sales.Customers AS c
JOIN Sales.Orders AS o ON c.CustomerID = o.CustomerID
JOIN Sales.Invoices AS i ON o.OrderID = i.OrderID
JOIN Sales.InvoiceLines AS il ON i.InvoiceID = il.InvoiceID
JOIN Warehouse.StockItems AS si ON il.StockItemID = si.StockItemID;
```
