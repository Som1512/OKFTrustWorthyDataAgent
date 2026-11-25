---
type: Dataset
title: WideWorldImporters
description: Enterprise B2B wholesale novelty goods importer and distributor dataset spanning Application, Purchasing, Sales, and Warehouse domains.
resource: WideworldimportersData/
tags: [wideworldimporters, wholesale, erp, data-warehouse]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

**WideWorldImporters** is a comprehensive B2B wholesale import and distribution dataset consisting of **48 CSV tables** (~252.2 MB uncompressed) organized across four logical schemas (`Application`, `Purchasing`, `Sales`, and `Warehouse`), including system-versioned temporal `_Archive` tables.

# Domain Schemas

## Application Schema (15 tables)
Shared reference data, geographic hierarchies, people/employees, payment/delivery lookup tables, and system parameters:
- [Application.Cities](/tables/application_cities.md) (37,940 rows)
- [Application.Cities_Archive](/tables/application_cities_archive.md) (28 rows)
- [Application.Countries](/tables/application_countries.md) (190 rows)
- [Application.Countries_Archive](/tables/application_countries_archive.md) (37 rows)
- [Application.DeliveryMethods](/tables/application_delivery_methods.md) (10 rows)
- [Application.DeliveryMethods_Archive](/tables/application_delivery_methods_archive.md) (1 rows)
- [Application.PaymentMethods](/tables/application_payment_methods.md) (4 rows)
- [Application.PaymentMethods_Archive](/tables/application_payment_methods_archive.md) (1 rows)
- [Application.People](/tables/application_people.md) (1,111 rows)
- [Application.People_Archive](/tables/application_people_archive.md) (961 rows)
- [Application.StateProvinces](/tables/application_state_provinces.md) (53 rows)
- [Application.StateProvinces_Archive](/tables/application_state_provinces_archive.md) (104 rows)
- [Application.SystemParameters](/tables/application_system_parameters.md) (148 rows)
- [Application.TransactionTypes](/tables/application_transaction_types.md) (13 rows)
- [Application.TransactionTypes_Archive](/tables/application_transaction_types_archive.md) (1 rows)

## Purchasing Schema (7 tables)
Vendor master records, supplier categories, purchase orders, line items, and accounts payable transactions:
- [Purchasing.PurchaseOrderLines](/tables/purchasing_purchase_order_lines.md) (8,367 rows)
- [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) (2,074 rows)
- [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md) (9 rows)
- [Purchasing.SupplierCategories_Archive](/tables/purchasing_supplier_categories_archive.md) (1 rows)
- [Purchasing.SupplierTransactions](/tables/purchasing_supplier_transactions.md) (2,438 rows)
- [Purchasing.Suppliers](/tables/purchasing_suppliers.md) (13 rows)
- [Purchasing.Suppliers_Archive](/tables/purchasing_suppliers_archive.md) (13 rows)

## Sales Schema (12 tables)
Customer accounts, buying groups, sales orders, fulfillment, customer invoices, credit notes, promotional deals, and accounts receivable ledger:
- [Sales.BuyingGroups](/tables/sales_buying_groups.md) (2 rows)
- [Sales.BuyingGroups_Archive](/tables/sales_buying_groups_archive.md) (0 rows)
- [Sales.CustomerCategories](/tables/sales_customer_categories.md) (8 rows)
- [Sales.CustomerCategories_Archive](/tables/sales_customer_categories_archive.md) (1 rows)
- [Sales.CustomerTransactions](/tables/sales_customer_transactions.md) (97,147 rows)
- [Sales.Customers](/tables/sales_customers.md) (663 rows)
- [Sales.Customers_Archive](/tables/sales_customers_archive.md) (51 rows)
- [Sales.InvoiceLines](/tables/sales_invoice_lines.md) (228,265 rows)
- [Sales.Invoices](/tables/sales_invoices.md) (70,510 rows)
- [Sales.OrderLines](/tables/sales_order_lines.md) (231,412 rows)
- [Sales.Orders](/tables/sales_orders.md) (73,595 rows)
- [Sales.SpecialDeals](/tables/sales_special_deals.md) (2 rows)

## Warehouse Schema (14 tables)
Product catalog (SKUs), stock holdings, bin locations, stock groups, inventory movement transactions, and cold-chain temperature telemetry:
- [Warehouse.ColdRoomTemperatures](/tables/warehouse_cold_room_temperatures.md) (4 rows)
- [Warehouse.ColdRoomTemperatures_Archive](/tables/warehouse_cold_room_temperatures_archive.md) (1,200,000 rows)
- [Warehouse.Colors](/tables/warehouse_colors.md) (36 rows)
- [Warehouse.Colors_Archive](/tables/warehouse_colors_archive.md) (1 rows)
- [Warehouse.PackageTypes](/tables/warehouse_package_types.md) (14 rows)
- [Warehouse.PackageTypes_Archive](/tables/warehouse_package_types_archive.md) (0 rows)
- [Warehouse.StockGroups](/tables/warehouse_stock_groups.md) (10 rows)
- [Warehouse.StockGroups_Archive](/tables/warehouse_stock_groups_archive.md) (1 rows)
- [Warehouse.StockItemHoldings](/tables/warehouse_stock_item_holdings.md) (227 rows)
- [Warehouse.StockItemStockGroups](/tables/warehouse_stock_item_stock_groups.md) (442 rows)
- [Warehouse.StockItemTransactions](/tables/warehouse_stock_item_transactions.md) (236,667 rows)
- [Warehouse.StockItems](/tables/warehouse_stock_items.md) (227 rows)
- [Warehouse.StockItems_Archive](/tables/warehouse_stock_items_archive.md) (444 rows)
- [Warehouse.VehicleTemperatures](/tables/warehouse_vehicle_temperatures.md) (65,998 rows)

# Related Concepts

- [Business Metrics](/metrics/index.md)
- [Canonical Join Paths](/joins/index.md)
