---
type: Table
title: Sales.SpecialDeals
description: Promotional pricing rules, percentage discounts, and fixed-price deals scoped by customer, buying group, or stock group.
resource: WideworldimportersData/Sales.SpecialDeals.csv
dataset: /datasets/wideworldimporters.md
schema: sales
row_count: 2
tags: [wideworldimporters, sales, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Promotional pricing rules, percentage discounts, and fixed-price deals scoped by customer, buying group, or stock group. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`sales` schema), containing **2** rows and **14** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `SpecialDealID` | INT64 | Primary key identifier. |
| `StockItemID` | STRING | Foreign key referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `CustomerID` | STRING | Foreign key referencing `CustomerID` in [Sales.Customers](/tables/sales_customers.md). |
| `BuyingGroupID` | INT64 | Foreign key referencing `BuyingGroupID` in [Sales.BuyingGroups](/tables/sales_buying_groups.md). |
| `CustomerCategoryID` | STRING | Foreign key referencing `CustomerCategoryID` in [Sales.CustomerCategories](/tables/sales_customer_categories.md). |
| `StockGroupID` | INT64 | Foreign key referencing `StockGroupID` in [Warehouse.StockGroups](/tables/warehouse_stock_groups.md). |
| `DealDescription` | STRING | Attribute `DealDescription` of `Sales.SpecialDeals`. |
| `StartDate` | STRING | Attribute `StartDate` of `Sales.SpecialDeals`. |
| `EndDate` | STRING | Attribute `EndDate` of `Sales.SpecialDeals`. |
| `DiscountAmount` | STRING | Attribute `DiscountAmount` of `Sales.SpecialDeals`. |
| `DiscountPercentage` | FLOAT64 | Attribute `DiscountPercentage` of `Sales.SpecialDeals`. |
| `UnitPrice` | STRING | Attribute `UnitPrice` of `Sales.SpecialDeals`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `LastEditedWhen` | STRING | Timestamp when the record was last modified. |

# Joins

- Joined with [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Sales.Customers](/tables/sales_customers.md) on `CustomerID`.
- Joined with [Sales.BuyingGroups](/tables/sales_buying_groups.md) on `BuyingGroupID`.
- Joined with [Sales.CustomerCategories](/tables/sales_customer_categories.md) on `CustomerCategoryID`.
- Joined with [Warehouse.StockGroups](/tables/warehouse_stock_groups.md) on `StockGroupID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
