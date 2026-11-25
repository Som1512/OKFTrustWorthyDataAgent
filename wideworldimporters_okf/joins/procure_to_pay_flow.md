---
type: JoinPath
title: Procure-to-Pay Join Path
description: Canonical join path connecting suppliers, purchase orders, stock receipts, and supplier ledger transactions.
resource: WideworldimportersData/Purchasing.PurchaseOrders.csv
tags: [joins, purchasing, procure-to-pay, supply-chain]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Connects vendor master records with outbound purchase orders, line-level stock receipts, warehouse inventory movements, and accounts payable transactions.

# Join Graph

1. [Purchasing.Suppliers](/tables/purchasing_suppliers.md) (`SupplierID`) → [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) (`SupplierID`)
2. [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) (`PurchaseOrderID`) → [Purchasing.PurchaseOrderLines](/tables/purchasing_purchase_order_lines.md) (`PurchaseOrderID`)
3. [Purchasing.PurchaseOrderLines](/tables/purchasing_purchase_order_lines.md) (`StockItemID`) → [Warehouse.StockItems](/tables/warehouse_stock_items.md) (`StockItemID`)
4. [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) (`PurchaseOrderID`) → [Purchasing.SupplierTransactions](/tables/purchasing_supplier_transactions.md) (`PurchaseOrderID`)
5. [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) (`PurchaseOrderID`) → [Warehouse.StockItemTransactions](/tables/warehouse_stock_item_transactions.md) (`PurchaseOrderID`)
