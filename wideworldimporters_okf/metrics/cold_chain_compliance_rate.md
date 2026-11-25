---
type: Metric
title: Cold-Chain Temperature Compliance Rate
description: Share of cold room and refrigerated vehicle sensor readings within safe chilled operating thresholds (0°C to 5°C).
resource: WideworldimportersData/Warehouse.ColdRoomTemperatures.csv
tags: [metric, warehouse, iot, cold-chain]
timestamp: 2026-11-23T15:38:00Z
---

# Definition

**Cold-Chain Temperature Compliance Rate** monitors sensor telemetry in [Warehouse.ColdRoomTemperatures_Archive](/tables/warehouse_cold_room_temperatures_archive.md) and [Warehouse.VehicleTemperatures](/tables/warehouse_vehicle_temperatures.md) to ensure chilled goods remain within safe temperature bounds (`0.0°C` to `5.0°C`).

# Calculation

```sql
SELECT
  ColdRoomSensorNumber,
  COUNT(CASE WHEN Temperature BETWEEN 0.0 AND 5.0 THEN 1 END) * 1.0 / COUNT(*) AS compliance_rate
FROM Warehouse.ColdRoomTemperatures_Archive
GROUP BY ColdRoomSensorNumber;
```

# Source Tables & Columns

- [Warehouse.ColdRoomTemperatures_Archive](/tables/warehouse_cold_room_temperatures_archive.md): `ColdRoomSensorNumber`, `Temperature`, `RecordedWhen`
- [Warehouse.VehicleTemperatures](/tables/warehouse_vehicle_temperatures.md): `VehicleRegistration`, `ChillerSensorNumber`, `Temperature`, `RecordedWhen`
