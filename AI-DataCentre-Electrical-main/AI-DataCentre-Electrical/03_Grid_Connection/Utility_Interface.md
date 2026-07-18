# Title: Utility Interface & Grid Connection (HT Incoming)
## Purpose: To define the engineering requirements for connecting the {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA facility to the {{cookiecutter.utility_provider}} grid in {{cookiecutter.state}}.
## Tags: #GridConnection #UtilityInterface #HT-Yard #{{cookiecutter.utility_provider}} #{{cookiecutter.utility_voltage_kv}}kV
## Standards Covered: Local Grid Codes, IEEE 1547, IEC 62271

---

## 1. Overview
For the {{cookiecutter.project_name}} project, the utility interface is the most critical single point of failure. Delivering {{cookiecutter.it_capacity_mw}} MW of IT load plus cooling demands a connection at **{{cookiecutter.utility_voltage_kv}}kV**. This file covers the transition from the {{cookiecutter.utility_provider}} Point of Common Coupling (PCC) to the Data Centre HT Yard.

## 2. Technical Requirements at PCC (Point of Common Coupling)
### 2.1 Power Quality Limits (IEEE 519 / Local Code)
As a massive consumer, the AI data centre must not pollute the {{cookiecutter.state}} utility grid.
*   **Voltage THD:** < 3%.
*   **Current THD:** < 5%.
*   **Voltage Unbalance:** < 1%.

### 2.2 Short Circuit Levels
*   **Design Basis:** Based on data from the local {{cookiecutter.city}} substation. Assume a stiff grid with high X/R ratio.
*   **Action:** All {{cookiecutter.utility_voltage_kv}}kV HT breakers (SF6 or Vacuum) must be rated to safely interrupt this fault level.

## 3. Engineering Workflow for Grid Integration
### Step 1: Load Sanction & Feasibility Study
*   Submit the formal demand application to {{cookiecutter.utility_provider}}.
*   Conduct a **Load Flow & Grid Stability Study** to ensure the {{cookiecutter.it_capacity_mw}} MW AI step-loads don't cause a voltage dip on the utility's transmission bus.

### Step 2: HT Yard / Substation Design
*   **Type:** Outdoor AIS (Air Insulated) or Indoor GIS (Gas Insulated). *Note: GIS is preferred for hyperscale footprint optimization.*
*   **Components:** 
    1.  **Lightning Arrestors (LA):** Station Class, Gapless ZnO type.
    2.  **Isolators:** With Earth Switch (Motorized for remote SCADA operation).
    3.  **Instrument Transformers:** CTs (Accuracy Class 0.2s for billing) and PTs.
    4.  **HT Metering:** Check Meter and Standby Meter as per local statutory regulations.

### Step 3: Protection & Coordination
*   **Main Protection:** Differential Protection (87T) and Distance Protection (21).
*   **Backup:** Overcurrent (50/51) and Earth Fault (50N/51N).
*   **Inter-tripping:** A dedicated fiber optic link (OPGW) between the DC and the {{cookiecutter.utility_provider}} Substation for "Transfer Trip" signals.

## 4. AI-Ready Infrastructure Considerations
*   **Fast Transient Recovery:** High-density {{cookiecutter.ai_silicon_vendor}} training causes massive load fluctuations. The utility transformer tap changers (OLTC) must be high-speed, or the facility UPS must actively filter this to prevent "Utility Flicker" complaints on the local {{cookiecutter.city}} grid.
*   **Renewable Energy (Open Access):** The utility interface must support **Open Access** billing to credit solar/wind energy generated off-site, aligning with hyperscaler ESG goals.

## 5. Construction & Commissioning Sequence
1.  **Civil Foundation:** Casting of Transformer pads and GIS room.
2.  **Equipment Erection:** Installation of Breakers and CT/PTs.
3.  **Cable Termination:** Stress-cone terminations for HT XLPE cables.
4.  **Pre-commissioning Tests:**
    *   Insulation Resistance (Megger).
    *   Contact Resistance (Ductor test).
    *   Hi-Pot Test (Power frequency voltage withstand).
5.  **Final Inspection:** AHJ / Electrical Inspector site visit.

## 6. Failure Modes & Risks
*   **Insulation Flashover:** Due to local environmental pollution in {{cookiecutter.city}}. *Mitigation:* Use polymer insulators with higher creepage distance.
*   **Cable Dig-up:** External contractors hitting the {{cookiecutter.utility_voltage_kv}}kV lines. *Mitigation:* Concrete encasement and marker tiles.
