# Elastic-Defend: Unified EDR & Scalable Detection Engineering

## 1. Project Overview
This repository documents the transition from traditional HIDS to a unified **Elastic Agent** architecture. By leveraging **Elastic Fleet Management**, I centralized the security policies for Windows and Linux endpoints, emphasizing "Detection Engineering" by tuning threshold-based rules for real-time alerting.

## 2. Technical Stack
* **SIEM:** Elastic Cloud (v8.x)
* **Agent:** Elastic Agent (Binary/ZIP Deployment)
* **Modules:** Elastic Defend (EDR), Windows System Integration
* **Framework:** MITRE ATT&CK Mapping



## 3. Implementation Phases

### Phase 1: Fleet Orchestration & Deployment
* Instead of standard MSI installers, I utilized a **Binary (ZIP) deployment** via PowerShell to ensure real-time installation logging.
* Configured an **Agent Policy** including "Elastic Defend" for kernel-level visibility.
* **Evidence:** ![PowerShell window showing 'Elastic Agent successfully installed’](./img/screenshot(2013).png)

### Phase 2: Detection Engineering (Custom Rule Creation)
* Engineered a **Custom Threshold Rule** to mitigate false negatives in Windows-specific SSH attacks.
* **Logic:** Filtered for `winlog.event_id : 4625` with a threshold of 3 failures per minute.
* **Evidence:** ![SCREENSHOT: Elastic Rule Editor showing the custom query](./img/screenshot(2008).png),![SCREENSHOT](./img/screenshot(2014).png)

### Phase 3: Alert Validation
* Validated the detection pipeline by re-running the Hydra brute-force simulation.
* Confirmed the rule triggered a severity alert in the **Security Alerts** dashboard.
* **Evidence:** [SCREENSHOT: Elastic Alerts dashboard showing](./img/screenshot(2015).png),![SCREENSHOT](./img/screenshot(2016).png)

## 4. Troubleshooting & Engineering Insights
A significant portion of this project involved resolving **Data Ingestion Gaps**. I performed a schema audit to align rule logic with the `winlog` and `logs-*` index patterns, ensuring telemetry from the Windows agent correctly mapped to the SIEM's detection engine.
*![SCREENSHOT: The "Under the Hood" JSON](./img/screenshot(2004).png), ![SCREENSHOT](./img/screenshot(2018).png)
