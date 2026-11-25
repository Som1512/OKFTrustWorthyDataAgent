---
type: Index
title: Tables Index
description: Complete catalog of all 48 active and system-versioned temporal archive tables in WideWorldImporters.
tags: [index, tables, schema]
timestamp: 2026-11-23T15:38:00Z
---

# Tables Directory

| Table | Schema | Row Count | Description |
| --- | --- | --- | --- |
| [Application.Cities](/tables/application_cities.md) | Application | 37,940 | Reference table of cities across states/provinces with spatial coordinates and recorded population. |
| [Application.Cities_Archive](/tables/application_cities_archive.md) | Application | 28 | System-versioned temporal archive preserving historical versions of city records. |
| [Application.Countries](/tables/application_countries.md) | Application | 190 | Reference table of sovereign nations and territories including ISO codes, regions, population, and geographic borders. |
| [Application.Countries_Archive](/tables/application_countries_archive.md) | Application | 37 | System-versioned temporal archive preserving historical versions of country records. |
| [Application.DeliveryMethods](/tables/application_delivery_methods.md) | Application | 10 | Lookup table defining shipping and freight delivery methods used for customer and supplier orders. |
| [Application.DeliveryMethods_Archive](/tables/application_delivery_methods_archive.md) | Application | 1 | System-versioned temporal archive preserving historical versions of delivery methods. |
| [Application.PaymentMethods](/tables/application_payment_methods.md) | Application | 4 | Lookup table defining accepted payment methods for customer receipts and supplier disbursements. |
| [Application.PaymentMethods_Archive](/tables/application_payment_methods_archive.md) | Application | 1 | System-versioned temporal archive preserving historical versions of payment methods. |
| [Application.People](/tables/application_people.md) | Application | 1,111 | Directory of employees, salespersons, system users, and external customer/supplier contacts. |
| [Application.People_Archive](/tables/application_people_archive.md) | Application | 961 | System-versioned temporal archive preserving historical changes to people and user records. |
| [Application.StateProvinces](/tables/application_state_provinces.md) | Application | 53 | Reference table of states, provinces, and territories mapped to countries and sales territories. |
| [Application.StateProvinces_Archive](/tables/application_state_provinces_archive.md) | Application | 104 | System-versioned temporal archive preserving historical versions of state/province records. |
| [Application.SystemParameters](/tables/application_system_parameters.md) | Application | 148 | Global application configuration, corporate headquarters addresses, and system settings. |
| [Application.TransactionTypes](/tables/application_transaction_types.md) | Application | 13 | Lookup table categorizing financial and inventory transaction types across ledger and stock movements. |
| [Application.TransactionTypes_Archive](/tables/application_transaction_types_archive.md) | Application | 1 | System-versioned temporal archive preserving historical versions of transaction types. |
| [Purchasing.PurchaseOrderLines](/tables/purchasing_purchase_order_lines.md) | Purchasing | 8,367 | Line-item details for supplier purchase orders, tracking ordered/received outer packages and expected unit prices. |
| [Purchasing.PurchaseOrders](/tables/purchasing_purchase_orders.md) | Purchasing | 2,074 | Header records for purchase orders placed with external suppliers, including expected delivery and finalization status. |
| [Purchasing.SupplierCategories](/tables/purchasing_supplier_categories.md) | Purchasing | 9 | Classification categories for grouping suppliers (e.g., Novelty Goods Supplier, Packaging Supplier). |
| [Purchasing.SupplierCategories_Archive](/tables/purchasing_supplier_categories_archive.md) | Purchasing | 1 | System-versioned temporal archive preserving historical versions of supplier categories. |
| [Purchasing.SupplierTransactions](/tables/purchasing_supplier_transactions.md) | Purchasing | 2,438 | Financial ledger entries recording supplier invoices, payments, credits, and outstanding balances. |
| [Purchasing.Suppliers](/tables/purchasing_suppliers.md) | Purchasing | 13 | Master directory of vendors and suppliers including banking details, payment terms, contacts, and addresses. |
| [Purchasing.Suppliers_Archive](/tables/purchasing_suppliers_archive.md) | Purchasing | 13 | System-versioned temporal archive preserving historical versions of supplier master records. |
| [Sales.BuyingGroups](/tables/sales_buying_groups.md) | Sales | 2 | Corporate retail chains or buying groups that aggregate multiple customer accounts. |
| [Sales.BuyingGroups_Archive](/tables/sales_buying_groups_archive.md) | Sales | 0 | System-versioned temporal archive preserving historical versions of buying groups. |
| [Sales.CustomerCategories](/tables/sales_customer_categories.md) | Sales | 8 | Classification segments for customers (e.g., Supermarket, Novelty Shop, Gift Store). |
| [Sales.CustomerCategories_Archive](/tables/sales_customer_categories_archive.md) | Sales | 1 | System-versioned temporal archive preserving historical versions of customer categories. |
| [Sales.CustomerTransactions](/tables/sales_customer_transactions.md) | Sales | 97,147 | Accounts receivable financial ledger recording customer invoices, payments, refunds, and balances. |
| [Sales.Customers](/tables/sales_customers.md) | Sales | 663 | Master directory of B2B customers including billing relationships, credit limits, payment days, and delivery runs. |
| [Sales.Customers_Archive](/tables/sales_customers_archive.md) | Sales | 51 | System-versioned temporal archive preserving historical versions of customer master records. |
| [Sales.InvoiceLines](/tables/sales_invoice_lines.md) | Sales | 228,265 | Granular line items for customer invoices including quantities, unit prices, tax amounts, extended prices, and line profit. |
| [Sales.Invoices](/tables/sales_invoices.md) | Sales | 70,510 | Header records for customer sales invoices and credit notes, tracking fulfillment, delivery confirmation, and dry/chiller counts. |
| [Sales.OrderLines](/tables/sales_order_lines.md) | Sales | 231,412 | Line-item details for customer sales orders including ordered quantities, picked quantities, and unit pricing. |
| [Sales.Orders](/tables/sales_orders.md) | Sales | 73,595 | Header records for incoming customer sales orders, backorder links, picking timestamps, and delivery instructions. |
| [Sales.SpecialDeals](/tables/sales_special_deals.md) | Sales | 2 | Promotional pricing rules, percentage discounts, and fixed-price deals scoped by customer, buying group, or stock group. |
| [Warehouse.ColdRoomTemperatures](/tables/warehouse_cold_room_temperatures.md) | Warehouse | 4 | Current real-time temperature telemetry readings from warehouse cold room sensors. |
| [Warehouse.ColdRoomTemperatures_Archive](/tables/warehouse_cold_room_temperatures_archive.md) | Warehouse | 1,200,000 | High-volume historical archive of cold room temperature sensor telemetry readings. |
| [Warehouse.Colors](/tables/warehouse_colors.md) | Warehouse | 36 | Lookup table of standard product colors assigned to stock items. |
| [Warehouse.Colors_Archive](/tables/warehouse_colors_archive.md) | Warehouse | 1 | System-versioned temporal archive preserving historical versions of product colors. |
| [Warehouse.PackageTypes](/tables/warehouse_package_types.md) | Warehouse | 14 | Lookup table of unit and outer packaging types (e.g., Each, Carton, Box, Packet). |
| [Warehouse.PackageTypes_Archive](/tables/warehouse_package_types_archive.md) | Warehouse | 0 | System-versioned temporal archive preserving historical versions of package types. |
| [Warehouse.StockGroups](/tables/warehouse_stock_groups.md) | Warehouse | 10 | Product catalog categories/groups used for merchandising and promotional targeting. |
| [Warehouse.StockGroups_Archive](/tables/warehouse_stock_groups_archive.md) | Warehouse | 1 | System-versioned temporal archive preserving historical versions of stock groups. |
| [Warehouse.StockItemHoldings](/tables/warehouse_stock_item_holdings.md) | Warehouse | 227 | Current inventory levels, bin locations, last cost price, reorder thresholds, and target stock levels per item. |
| [Warehouse.StockItemStockGroups](/tables/warehouse_stock_item_stock_groups.md) | Warehouse | 442 | Many-to-many junction table mapping stock items to one or more product stock groups. |
| [Warehouse.StockItemTransactions](/tables/warehouse_stock_item_transactions.md) | Warehouse | 236,667 | Inventory movement ledger tracking stock receipts, customer shipments, and stock adjustments. |
| [Warehouse.StockItems](/tables/warehouse_stock_items.md) | Warehouse | 227 | Master product catalog containing SKUs, pricing, tax rates, chiller requirements, packaging specs, and supplier links. |
| [Warehouse.StockItems_Archive](/tables/warehouse_stock_items_archive.md) | Warehouse | 444 | System-versioned temporal archive preserving historical versions of product catalog records. |
| [Warehouse.VehicleTemperatures](/tables/warehouse_vehicle_temperatures.md) | Warehouse | 65,998 | Cold-chain telemetry log recording chiller temperatures inside refrigerated delivery vehicles. |
