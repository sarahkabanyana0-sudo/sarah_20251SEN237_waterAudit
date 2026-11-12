# Urban Water Distribution Leakage and Meter Reading Audit Platform

| | |
|---|---|
| **Student** | Kabanyana Sarah |
| **Student ID** | 20251SEN237 |
| **Course** | Database Development with PL/SQL |
| **Instructor** | Eric Maniraguha |
| **Repository** | `sarah_20251SEN237_waterAudit` |
| **Phase** | 0 - Research, data source and proposal |

## Problem statement
Water utilities lose a large share of the water they produce through leaking pipes, faulty or tampered meters and unrecorded consumption. In Rwanda, the Auditor General reported that 37.8% of the water WASAC produced in FY2024/25 was not billed (85.75 million m3 produced, 53.33 million m3 billed), valued at about Rwf10.4 billion. The same audit found defective meters replaced 12 to 269 days late. Leak detection research exists, but utilities lack a structured database that links meter readings, leak events, alerts and repair work with a full audit trail.

## Objectives
**Main objective:** Design and build an Oracle PL/SQL database that detects suspicious meter readings and probable leaks in an urban water network and tracks each one through to repair, with every change audited.

**Specific objectives**
1. Normalise raw SCADA, smart-meter and leak data into 3NF Oracle tables.
2. Validate meter readings and flag anomalies (negative, flat-line, spike, abnormal night flow) using PL/SQL procedures, functions and cursors.
3. Calculate zone-level non-revenue-water (NRW) indicators and raise alerts automatically.
4. Enforce business rules and a restriction rule with triggers, and record all data changes in an audit log.
5. Provide an Oracle APEX interface connected to the live database for field officers and managers.

## Data source
- **BattLeDIM dataset** (Vrachimis et al., 2020), Zenodo, DOI [10.5281/zenodo.4017659](https://doi.org/10.5281/zenodo.4017659), licence **CC BY 4.0**.
- Contents used: 2018 and 2019 demand readings from 82 automated meter reading (AMR) devices (L/h), 33 pressure sensors, 3 flow sensors, 1 tank level sensor, labelled leak time series and the L-Town EPANET network file.
- Size: roughly 105,000 five-minute readings per meter per year. Raw files are about 550 MB, so the raw files are **not** stored in this repo; see `data/README.md`. Readings are aggregated to hourly values (about 718,000 meter readings per year) for loading.
- Contains no personal information. All meters are identified by node IDs only.
- **Data note:** L-Town is a hypothetical town whose network and measurements were generated from a real water network in a city in Cyprus. Real Rwandan NRW statistics (Auditor General FY2024/25 and published WASAC figures) are added as a small benchmark table.

## Innovation
**Option:** User interface (with dashboard pages). **Tool:** Oracle APEX.
An APEX application connected to the Oracle database lets a field officer record a meter reading and a technician close a work order by calling PL/SQL procedures, while a manager sees a live dashboard of open leak alerts and zone NRW. Business rules stay in PL/SQL; APEX only displays data and calls procedures.

## Planned tables (3NF)
`ZONE`, `METER`, `METER_READING`, `SENSOR`, `SENSOR_READING`, `PIPE`, `LEAK_EVENT`, `ALERT`, `WORK_ORDER`, `TECHNICIAN`, `HOLIDAY`, `NRW_BENCHMARK`, `AUDIT_LOG`

## Planned PL/SQL features
| Feature | Where it is used |
|---|---|
| Procedure `record_reading` | Inserts a validated meter reading and raises an alert if it is suspicious |
| Procedure `open_work_order` / `close_work_order` | Moves a leak alert through the repair workflow |
| Function `zone_nrw_pct` | Returns NRW % for a zone and period |
| Function `leak_risk_score` | Scores a meter or zone from night flow and pressure drop |
| Explicit cursor with `BULK COLLECT` | Nightly scan of all meters for flat-line and zero-flow runs |
| Analytic SQL (`LAG`) | Detects sudden jumps between consecutive readings |
| Package `pkg_meter_audit` | Groups validation and anomaly procedures |
| Package `pkg_leak_mgmt` | Groups leak, alert and work-order logic |
| Trigger (before insert/update on `METER_READING`) | Blocks negative or impossible readings |
| Trigger (restriction rule) | Blocks changes to readings and work orders on weekends and public holidays |
| Trigger (on `LEAK_EVENT`) | Prevents closing a leak while its work order is still open |
| Audit triggers | Write every insert, update and delete to `AUDIT_LOG`, including denied attempts |
| Exception handling | Custom exceptions such as `invalid_reading_ex` and `duplicate_reading_ex` |
| `DBMS_SCHEDULER` job | Runs the nightly audit automatically |

## Repository structure
```
docs/research/       research log
docs/proposal/       2-page proposal
docs/presentation/   12-slide presentation
data/                dataset instructions (raw files not stored)
```

## References
- Min, K. W., Kim, T., Lee, S., Choi, Y. H., & Kim, J. H. (2022). Detecting and localizing leakages in water distribution systems using a two-phase model. *Journal of Water Resources Planning and Management, 148*(10), Article 04022051.
- Mwitirehe, J., Kipruto, C. W., & Ruranga, C. (2024). Analyzing non-revenue water dynamics in Rwanda: Leveraging machine learning predictive modeling for comprehensive insights and mitigation strategies. *Water Practice and Technology, 19*(6), 2376-2398. https://doi.org/10.2166/wpt.2024.145
- KT Press Staff Writer. (2026, October 20). Why did WASAC halt water monitoring project despite 99% completion? *KT Press*. https://www.ktpress.rw/2026/10/why-did-wasac-halt-water-monitoring-project-despite-99-completion/
- Nyandwi, C. (2026, October 21). Rwanda: Prepaid water system set for wider household rollout in 2027. *The New Times*. https://allafrica.com/stories/202610220023.html
- Oracle. (n.d.). DBMS_SCHEDULER. In *Oracle Database PL/SQL Packages and Types Reference* (11g Release 2). https://docs.oracle.com/cd/E24693_01/appdev.11203/e23448/d_sched.htm
- Vrachimis, S. G., Eliades, D. G., Taormina, R., Kapelan, Z., Ostfeld, A., Liu, S., Kyriakou, M., Pavlou, P., Qiu, M., & Polycarpou, M. M. (2022). Battle of the leakage detection and isolation methods. *Journal of Water Resources Planning and Management, 148*(12), Article 04022068. https://doi.org/10.1061/(ASCE)WR.1943-5452.0001601
- Vrachimis, S. G., Eliades, D. G., Taormina, R., Ostfeld, A., Kapelan, Z., Liu, S., Kyriakou, M., Pavlou, P., Qiu, M., & Polycarpou, M. (2020). *Dataset of BattLeDIM: Battle of the leakage detection and isolation methods* (Version v1) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.4017659
