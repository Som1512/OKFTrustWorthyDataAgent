---
type: Table
title: Warehouse.StockItems_Archive
description: System-versioned temporal archive preserving historical versions of product catalog records.
resource: WideworldimportersData/Warehouse.StockItems_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 444
tags: [wideworldimporters, warehouse, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

System-versioned temporal archive preserving historical versions of product catalog records. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **444** rows and **25** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `StockItemID` | INT64 | Identifier referencing `StockItemID` in [Warehouse.StockItems](/tables/warehouse_stock_items.md). |
| `StockItemName` | STRING | Attribute `StockItemName` of `Warehouse.StockItems_Archive`. |
| `SupplierID` | INT64 | Foreign key referencing `SupplierID` in [Purchasing.Suppliers](/tables/purchasing_suppliers.md). |
| `ColorID` | STRING | Foreign key referencing `ColorID` in [Warehouse.Colors](/tables/warehouse_colors.md). |
| `UnitPackageID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `OuterPackageID` | INT64 | Foreign key referencing `PackageTypeID` in [Warehouse.PackageTypes](/tables/warehouse_package_types.md). |
| `Brand` | STRING | Attribute `Brand` of `Warehouse.StockItems_Archive`. |
| `Size` | STRING | Attribute `Size` of `Warehouse.StockItems_Archive`. |
| `LeadTimeDays` | INT64 | Attribute `LeadTimeDays` of `Warehouse.StockItems_Archive`. |
| `QuantityPerOuter` | INT64 | Attribute `QuantityPerOuter` of `Warehouse.StockItems_Archive`. |
| `IsChillerStock` | BOOL | Attribute `IsChillerStock` of `Warehouse.StockItems_Archive`. |
| `Barcode` | STRING | Attribute `Barcode` of `Warehouse.StockItems_Archive`. |
| `TaxRate` | FLOAT64 | Attribute `TaxRate` of `Warehouse.StockItems_Archive`. |
| `UnitPrice` | FLOAT64 | Attribute `UnitPrice` of `Warehouse.StockItems_Archive`. |
| `RecommendedRetailPrice` | FLOAT64 | Attribute `RecommendedRetailPrice` of `Warehouse.StockItems_Archive`. |
| `TypicalWeightPerUnit` | FLOAT64 | Attribute `TypicalWeightPerUnit` of `Warehouse.StockItems_Archive`. |
| `MarketingComments` | STRING | Attribute `MarketingComments` of `Warehouse.StockItems_Archive`. |
| `InternalComments` | STRING | Attribute `InternalComments` of `Warehouse.StockItems_Archive`. |
| `Photo` | STRING | Attribute `Photo` of `Warehouse.StockItems_Archive`. |
| `CustomFields` | STRING | Attribute `CustomFields` of `Warehouse.StockItems_Archive`. |
| `Tags` | STRING | Attribute `Tags` of `Warehouse.StockItems_Archive`. |
| `SearchDetails` | STRING | Attribute `SearchDetails` of `Warehouse.StockItems_Archive`. |
| `LastEditedBy` | INT64 | Foreign key referencing `PersonID` in [Application.People](/tables/application_people.md). |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Warehouse.StockItems](/tables/warehouse_stock_items.md) on `StockItemID`.
- Joined with [Purchasing.Suppliers](/tables/purchasing_suppliers.md) on `SupplierID`.
- Joined with [Warehouse.Colors](/tables/warehouse_colors.md) on `ColorID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `UnitPackageID = PackageTypeID`.
- Joined with [Warehouse.PackageTypes](/tables/warehouse_package_types.md) on `OuterPackageID = PackageTypeID`.
- Joined with [Application.People](/tables/application_people.md) on `LastEditedBy = PersonID`.
