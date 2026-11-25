---
type: Table
title: Warehouse.VehicleTemperatures
description: Cold-chain telemetry log recording chiller temperatures inside refrigerated delivery vehicles.
resource: WideworldimportersData/Warehouse.VehicleTemperatures.csv
dataset: /datasets/wideworldimporters.md
schema: warehouse
row_count: 65998
tags: [wideworldimporters, warehouse, active-table]
timestamp: 2026-11-23T15:38:00Z
---

# Overview

Cold-chain telemetry log recording chiller temperatures inside refrigerated delivery vehicles. Part of the [WideWorldImporters Dataset](/datasets/wideworldimporters.md) (`warehouse` schema), containing **65,998** rows and **8** columns.

# Schema

| Column | Type | Description |
| --- | --- | --- |
| `VehicleTemperatureID` | INT64 | Primary key identifier. |
| `VehicleRegistration` | STRING | Attribute `VehicleRegistration` of `Warehouse.VehicleTemperatures`. |
| `ChillerSensorNumber` | INT64 | Attribute `ChillerSensorNumber` of `Warehouse.VehicleTemperatures`. |
| `RecordedWhen` | STRING | Attribute `RecordedWhen` of `Warehouse.VehicleTemperatures`. |
| `Temperature` | FLOAT64 | Attribute `Temperature` of `Warehouse.VehicleTemperatures`. |
| `FullSensorData` | STRING | Attribute `FullSensorData` of `Warehouse.VehicleTemperatures`. |
| `IsCompressed` | BOOL | Attribute `IsCompressed` of `Warehouse.VehicleTemperatures`. |
| `CompressedSensorData` | STRING | Attribute `CompressedSensorData` of `Warehouse.VehicleTemperatures`. |

# Joins

Standalone reference/telemetry table with no outbound foreign keys.
