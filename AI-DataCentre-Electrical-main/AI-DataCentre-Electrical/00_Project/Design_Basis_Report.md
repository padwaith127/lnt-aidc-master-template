# Title: Design Basis Report (DBR) - Electrical Systems
## Purpose: To establish the fundamental design parameters, assumptions, and criteria for the {{cookiecutter.it_capacity_mw}} MW AI-Ready Data Centre.
## Project: {{cookiecutter.project_name}}
## Tags: #DBR #DesignCriteria #Hyperscale #AI-Ready
## Standards Covered: Uptime Tier III, TIA-942-C, IEEE 3001.2, Local Electrical Codes

---

## 1. Introduction
The Design Basis Report (DBR) is the "Source of Truth" for the project. For the {{cookiecutter.project_name}} {{cookiecutter.it_capacity_mw}} MW facility, this document ensures the electrical infrastructure supports high-density transient loads of {{cookiecutter.ai_silicon_vendor}} clusters while maintaining hyperscale uptime.

## 2. Site Environmental Conditions ({{cookiecutter.city}}, {{cookiecutter.state}})
Design parameters account for the local environment of {{cookiecutter.city}}.

| Parameter | Value | Reference |
| :--- | :--- | :--- |
| **Max Ambient Temperature** | {{cookiecutter.max_ambient_temp}}°C | Local Data |
| **Design Ambient for Equipment** | {{cookiecutter.max_ambient_temp | int + 5}}°C (De-rating applied) | Manufacturer Standard |
| **Seismic Zone** | Site Specific | IS 1893 / IBC |

## 3. Power Requirements & Topology
### 3.1 Utility Connection
*   **Incoming Voltage:** {{cookiecutter.utility_voltage_kv}} kV (Dual Source from {{cookiecutter.utility_provider}}).
*   **Ultimate IT Load:** {{cookiecutter.it_capacity_mw}} MW.
*   **Total Facility Apparent Power:** ~{{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA.

### 3.2 Redundancy Architecture
*   **System Topology:** Distributed Redundant (N+1) or 2N (System+System).
*   **Tier Rating:** Uptime Tier III (Concurrent Maintainability). 

## 4. Electrical Design Criteria
| Parameter | Standard Value | Tolerance/Notes |
| :--- | :--- | :--- |
| **System Frequency** | 50 Hz / 60 Hz | AHJ Standard |
| **HT Voltage** | {{cookiecutter.utility_voltage_kv}} kV | +/- 10% |
| **Fault Level (LT)** | {{cookiecutter.fault_level_ka}} kA | 1 Second Duration |
| **Voltage Harmonic Distortion (THD-v)** | < 3% | IEEE 519 |
