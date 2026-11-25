---
type: Table
title: Warehouse.ColdRoomTemperatures
description: Current real-time temperature telemetry readings from warehouse cold room sensors.
resource: WideworldimportersData/Warehouse.ColdRoomTemperatures.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 4
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Current real-time temperature telemetry readings from warehouse cold room sensors. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **4** rows and **6** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `ColdRoomTemperatureID` | INT64 | Primary key identifier. |
| `ColdRoomSensorNumber` | INT64 | Attribute `ColdRoomSensorNumber` of `Warehouse.ColdRoomTemperatures`. |
| `RecordedWhen` | STRING | Attribute `RecordedWhen` of `Warehouse.ColdRoomTemperatures`. |
| `Temperature` | FLOAT64 | Attribute `Temperature` of `Warehouse.ColdRoomTemperatures`. |
| `ValidFrom` | STRING | System-versioned temporal row validity start timestamp (UTC). |
| `ValidTo` | STRING | System-versioned temporal row validity end timestamp (UTC). |

# Joins

- Historical row versions archived in [Warehouse.ColdRoomTemperatures_Archive](/tables/warehouse_cold_room_temperatures_archive.md) on `ColdRoomTemperatureID`.
