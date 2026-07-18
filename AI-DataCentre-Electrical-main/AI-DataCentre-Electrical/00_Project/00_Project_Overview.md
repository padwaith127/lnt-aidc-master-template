# Title: Project Overview - {{cookiecutter.it_capacity_mw}} MW AI-Ready Hyperscale DC
## Purpose: To define the technical scope and strategic objectives of the {{cookiecutter.project_name}}.
## Tags: #ProjectOverview #{{cookiecutter.it_capacity_mw}}MW #{{cookiecutter.city}} #{{cookiecutter.ai_silicon_vendor}}
## Standards Covered: Uptime Tier III, TIA-942-C

---

## 1. Project Introduction
The {{cookiecutter.project_name}} project at {{cookiecutter.city}}, {{cookiecutter.state}} is a state-of-the-art {{cookiecutter.it_capacity_mw}} MW IT-load hyperscale data centre. It is designed "AI-first," engineered to support the extreme power densities of {{cookiecutter.ai_silicon_vendor}} infrastructure.

## 2. Key Technical Specifications
* **Total IT Power:** {{cookiecutter.it_capacity_mw}} MW.
* **Location:** {{cookiecutter.city}}, {{cookiecutter.state}}.
* **Power Density:** AI Zones ranging from 40 kW to 120+ kW/rack (Liquid Cooled).
* **Redundancy:** Uptime Tier III (Concurrent Maintainability).
* **Incoming Utility:** {{cookiecutter.utility_voltage_kv}} kV (Dedicated Substation via {{cookiecutter.utility_provider}}).
* **Power Usage Effectiveness (PUE) Target:** < {{cookiecutter.target_pue}} (Annualized).

## 3. Engineering Workflow
The design follows a sequential "Outside-In" approach:
1.  **Utility Interface:** Securing capacity from {{cookiecutter.utility_provider}}.
2.  **HT Yard:** {{cookiecutter.utility_voltage_kv}} kV Substation design per local norms.
3.  **Transformation:** {{cookiecutter.utility_voltage_kv}} kV / 415V or 480V transformation.
4.  **Backup:** N+1 Diesel Generator sets.
