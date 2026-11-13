# Research Log

**Project:** Urban Water Distribution Leakage and Meter Reading Audit Platform
**Student:** Kabanyana Sarah (ID 20251SEN237) | **Course:** Database Development with PL/SQL
**Last updated:** 12 November 2026

| # | Source (APA) | Type | Link | Key finding | Gap it shows |
|---|--------------|------|------|-------------|--------------|
| 1 | Mwitirehe, J., Kipruto, C. W., & Ruranga, C. (2024). Analyzing non-revenue water dynamics in Rwanda: Leveraging machine learning predictive modeling for comprehensive insights and mitigation strategies. *Water Practice and Technology, 19*(6), 2376-2398. | Research paper | https://doi.org/10.2166/wpt.2024.145 | Rwanda's average NRW was 41.24% from July 2014 to June 2023, far above the 25% target. Kigali averaged 38.61% against 55.31% in Nyagatare, and no water supply met the target in more than 20% of the 36 quarters studied. | The study analyses NRW at network and quarterly level. It does not provide an operational system linking meter readings, leak events and repair work. |
| 2 | Vrachimis, S. G., Eliades, D. G., Taormina, R., Kapelan, Z., Ostfeld, A., Liu, S., Kyriakou, M., Pavlou, P., Qiu, M., & Polycarpou, M. M. (2022). Battle of the leakage detection and isolation methods. *Journal of Water Resources Planning and Management, 148*(12), Article 04022068. | Research paper | https://doi.org/10.1061/(ASCE)WR.1943-5452.0001601 | Summarises the BattLeDIM competition, where teams used SCADA flow and pressure data to detect leaks. The authors conclude that leak detection and isolation methods need further development and that more open benchmark problems are needed. | Algorithms output result files only. Nothing stores alerts, assigns repairs or keeps an audit trail of who changed what. |
| 3 | Min, K. W., Kim, T., Lee, S., Choi, Y. H., & Kim, J. H. (2022). Detecting and localizing leakages in water distribution systems using a two-phase model. *Journal of Water Resources Planning and Management, 148*(10), Article 04022051. | Research paper | https://pure.korea.ac.kr/en/publications/detecting-and-localizing-leakages-in-water-distribution-systems-u/ | A k-means plus emitter-coefficient method was tested on the BattLeDIM data. The abstract reports that none of the 23 real leakage events were detected or localised. | Purely algorithmic detection can miss leaks, so utilities also need rule-based checks and field confirmation recorded in a database. |
| 4 | KT Press Staff Writer. (2026, October 20). Why did WASAC halt water monitoring project despite 99% completion? *KT Press*. | Report / statistic (reporting the Auditor General's FY2024/25 findings) | https://www.ktpress.rw/2026/10/why-did-wasac-halt-water-monitoring-project-despite-99-completion/ | 37.8% of water WASAC produced was not billed (39.5% the year before). Of 85.75 million m3 produced, 53.33 million m3 was billed. Unbilled water was valued at Rwf10.4 billion. Defective meter replacements were delayed by 12 to 269 days. | The audit exposes losses and meter delays but no meter-level audit trail or leak-to-repair workflow is described. |
| 5 | Nyandwi, C. (2026, October 21). Rwanda: Prepaid water system set for wider household rollout in 2027. *The New Times* (via allAfrica). | Existing system | https://allafrica.com/stories/202610220023.html | WASAC's prepaid water pilot runs at about 200 public water points and is now being tested on household connections. The same article notes the government is turning to technology, including AI, to tackle NRW. The SCADA loss-monitoring project (source 4) was halted near completion. | The prepaid pilot targets billing and payment. No published system reconciles meter readings, flags suspicious readings and tracks leak repairs. |
| 6 | Vrachimis, S. G., Eliades, D. G., Taormina, R., Ostfeld, A., Kapelan, Z., Liu, S., Kyriakou, M., Pavlou, P., Qiu, M., & Polycarpou, M. (2020). *Dataset of BattLeDIM: Battle of the leakage detection and isolation methods* (Version v1) [Data set]. Zenodo. | **Dataset** | https://doi.org/10.5281/zenodo.4017659 | Licence CC BY 4.0. Contains 2018 and 2019 data: demand from 82 automated meter reading (AMR) devices (L/h), 33 pressure sensors, 3 flow sensors, 1 tank level sensor, leak time series and an EPANET network model. | Files only (CSV/XLSX/INP). There is no relational structure, business rules or audit trail. Note: L-Town is a hypothetical town generated from a real Cyprus network. |
| 7 | Oracle. (n.d.). DBMS_SCHEDULER. In *Oracle Database PL/SQL Packages and Types Reference* (11g Release 2). | Technical source | https://docs.oracle.com/cd/E24693_01/appdev.11203/e23448/d_sched.htm | CREATE_JOB lets the database run a stored procedure or PL/SQL block on a repeat schedule, which supports nightly leak and meter audits inside the database. | Switch this link to the documentation of the Oracle version you install (for example 19c) before submitting. |

## Honest reading status (update before submitting)

The rules say a fake or unread reference counts as plagiarism. Every link above was opened and checked to exist, but at the time of writing only these parts had been read:

- Sources 1, 2, 3, 6: abstract / record page (source 6 also its README). **Read the full text of 1 and 2 yourself before the presentation.**
- Source 4 and 5: full article text.
- Source 7: documentation excerpts.

Once you have read each one fully, add your own sentence under "My notes" below.

## My notes
(Add your own notes on each source here.)
