---
type: Table
title: Warehouse.StockItems
description: Master product catalog containing SKUs, pricing, tax rates, chiller requirements, packaging specs, and supplier links.
resource: WideworldimportersData/Warehouse.StockItems.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 227
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Master product catalog containing SKUs, pricing, tax rates, chiller requirements, packaging specs, and supplier links. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **227** rows and **25** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockItemID` | INT64 | Primary key identifier. |
| `StockItemName` | STRING | Attribute `StockItemName` of `Warehouse.StockItems`. |
| `SupplierID` | INT64 | Foreign key referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `ColorID` | STRING | Foreign key referencing `ColorID` in [Warehouse.Colors](/tables/warehouse_colors.md). |
| `UnitPackageID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `OuterPackageID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `Brand` | STRING | Attribute `Brand` of `Warehouse.StockItems`. |
| `Size` | STRING | Attribute `Size` of `Warehouse.StockItems`. |
| `LeadTimeDays` | INT64 | Attribute `LeadTimeDays` of `Warehouse.StockItems`. |
| `QuantityPerOuter` | INT64 | Attribute `QuantityPerOuter` of `Warehouse.StockItems`. |
| `IsChillerStock` | BOOL | Attribute `IsChillerStock` of `Warehouse.StockItems`. |
| `Barcode` | STRING | Attribute `Barcode` of `Warehouse.StockItems`. |
| `TaxRate` | FLOAT64 | Attribute `TaxRate` of `Warehouse.StockItems`. |
| `UnitPrice` | FLOAT64 | Attribute `UnitPrice` of `Warehouse.StockItems`. |
| `RecommendedRetailPrice` | FLOAT64 | Attribute `RecommendedRetailPrice` of `Warehouse.StockItems`. |
| `TypicalWeightPerUnit` | FLOAT64 | Attribute `TypicalWeightPerUnit` of `Warehouse.StockItems`. |
| `MarketingComments` | STRING | Attribute `MarketingComments` of `Warehouse.StockItems`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Warehouse.StockItems`. |
| `Photo` | STRING | Attribute `Photo` of `Warehouse.StockItems`. |
| `CustomFields` | STRING | Attribute `CustomFields` of `Warehouse.StockItems`. |
| `Tags` | STRING | Attribute `Tags` of `Warehouse.StockItems`. |
| `SearchDetails` | STRING | Attribute `SearchDetails` of `Warehouse.StockItems`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Joined with [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Warehouse.Colors](/tables/warehouse_colors.md) on `ColorID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `UnitPackageID = PackageTypeID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `OuterPackageID = PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
- Historical row versions archived in [Warehouse.StockItems_Archive](/tables/warehouse_stock_items_archive.md) on `StockItemID`.
