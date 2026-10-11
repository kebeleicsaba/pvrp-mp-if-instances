# PVRP-MP-IF Instances

Benchmark instances for the periodic vehicle routing problem with preferred pickup days, multiple service periods and intermediate facilities (PVRP-MP-IF). 
Authors: Csaba Kebelei, Balázs Dávid.

The instances are adapted from the PVRP-IF waste-collection instances of [Taverna and Tilk (2026)](https://doi.org/10.1016/j.ejor.2025.09.039), available at [iolab-uniud/pvrpif-instances](https://github.com/iolab-uniud/pvrpif-instances).

This repository contains the adapted literature benchmark instances (referred to as the *Taverna instances*) used in the paper:

> Kebelei, C., & Dávid, B. A periodic vehicle routing problem for waste collection with preferred pickup days and multiple service periods. *Manuscript under review.*

## Repository structure

```
taverna_horizon_4_balanced/
taverna_horizon_4_random/
taverna_horizon_6_balanced/
taverna_horizon_6_random/
```

Each folder contains the 40 original instances with the period length $|P|$ given in its name. For example, `adapted_Milano_020_4_0.geojson` is adapted from `Milano_020_4_0.geojson`.

The balanced and random versions of an instance differ only in the preferred days of the customers:

- **balanced**: preferred days cycle through all days in customer ID order.
- **random**: preferred days are chosen uniformly at random using seed 42 (files are processed alphabetically, with the four-day horizon first).

## Format

The files keep the original GeoJSON format. `...` marks unchanged original content.

```js
{
  "type": "FeatureCollection",
  "info": {
    ...,
    "planningHorizon": 4,
    "number_of_service_periods": 4,
    "deviation": 1,
    "max_time": 5
  },
  "features": [
    { ..., "properties": { "id": 0, "type": "depot", ... } },
    { ..., "properties": { "id": 1, "type": "customer", ..., "preferred_day": 1 } },
    ...
    { ..., "properties": { "id": 22, "type": "intermediateFacility", ... } }
  ],
  "duration": [[...], ...]
}
```

| Key | Notation | Meaning |
|---|:---:|---|
| `info.planningHorizon` | $\lvert P\rvert$ | days per period |
| `info.number_of_service_periods` | $N_P$ | number of periods |
| `info.deviation` | $\delta$ | maximum deviation from the preferred day (days) |
| `info.max_time` | $\Delta$ | maximum number of days between two consecutive visits |
| `properties.preferred_day` | $R_i$ | preferred day of customer $i$ in each period |

*Note: Each customer is served exactly once per period, so the original `frequency` and `totDemand` fields are not used.*
