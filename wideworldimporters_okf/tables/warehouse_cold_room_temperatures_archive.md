---
type: Table
title: Warehouse.ColdRoomTemperatures_Archive
description: High-volume historical archive of cold room temperature sensor telemetry readings.
resource: WideworldimportersData/Warehouse.ColdRoomTemperatures_Archive.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 1200000
tags: [wideworldimporters, warehouse, temporal-archive]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

High-volume historical archive of cold room temperature sensor telemetry readings. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **1,200,000** rows and **6** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `ColdRoomTemperatureID` | INT64 | Identifier referencing `ColdRoomTemperatureID` in [Warehouse.ColdRoomTemperatures](/tables/warehouse_cold_room_temperatures.md). |
| `ColdRoomSensorNumber` | INT64 | Attribute `ColdRoomSensorNumber` of `Warehouse.ColdRoomTemperatures_Archive`. |
| `RecordedWhen` | STRING | Attribute `RecordedWhen` of `Warehouse.ColdRoomTemperatures_Archive`. |
| `Temperature` | FLOAT64 | Attribute `Temperature` of `Warehouse.ColdRoomTemperatures_Archive`. |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Temporal history linked to active record [Warehouse.ColdRoomTemperatures](/tables/warehouse_cold_room_temperatures.md) on `ColdRoomTemperatureID`.
