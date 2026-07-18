# Title: Emergency Backup Generation - DG System Design
## Purpose: To define the engineering requirements for the standby power plant using Diesel/HVO Generators for the {{cookiecutter.project_name}}.
## Tags: #DieselGenerator #BackupPower #DCC-Rating #Hyperscale
## Standards Covered: ISO 8528, Emissions Standards, IEEE 446, NFPA 110

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW AI-ready facility, the Generator system is the ultimate guarantor of availability. It must be capable of supporting the full facility load (IT + Cooling + Ancillary) indefinitely during a {{cookiecutter.utility_provider}} failure. The system must handle massive load steps and maintain frequency stability to support UPS charging and AI Liquid Cooling operations.

## 2. Engineering Philosophy: The "Data Centre Continuous" (DCC) Rating
Traditional "Standby" or "Prime" ratings are insufficient for hyperscale DCs.
*   **DCC Rating (ISO 8528):** Defined by the Uptime Institute. It allows the generator to run at a constant or varying load for unlimited hours, specifically for data centre applications.
*   **Performance Class G3:** Mandatory for Data Centres. It defines strict limits on frequency and voltage deviations during load steps.

## 3. Equipment Selection & Sizing
### 3.1 Sizing Logic
For an IT load of {{cookiecutter.it_capacity_mw}} MW (~{{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float / 0.95) | round(2) }} MVA Total Load):
*   **Unit Sizing:** Typically use **3 MVA to 4 MVA** continuous units.
*   **Redundancy:** N+1 or N+2 at the "Block" or "System" level.

### 3.2 Derating Factors ({{cookiecutter.city}} Context)
The nameplate rating must be derated for local conditions:
1.  **Ambient Temperature:** {{cookiecutter.max_ambient_temp}}°C (requires oversized radiators).
2.  **Altitude:** Site Specific.
3.  **Humidity:** Requires anti-condensation heaters in the alternator.

## 4. Engineering Calculations: Step Load & Autonomy
### 4.1 Step Load Calculation
AI clusters cause high "Step Loads" during recovery.
*   **Requirement:** The DG must accept 60% of its rated load in the first step without the frequency dropping below 45 Hz (per ISO 8528-5).

### 4.2 Fuel Autonomy Calculation
*   **Assumption:** Total active power $\approx$ {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float) | round(2) }} MW.
*   **Fuel Consumption:** ~200 Liters/Hour per MW of load.
*   **Calculation for 48 Hours:** 
    $$V_{fuel} = {{ (cookiecutter.it_capacity_mw | float * cookiecutter.target_pue | float) | round(2) }} \times 200 \times 48 \approx \text{Total Liters}$$

## 5. AI-Ready Design Features
1.  **Fast Start-Up:** "Black Start" to "Ready-to-Load" in **< 15 seconds**. Critical as Lithium-ion UPS runtimes are sized for only 5-10 minutes.
2.  **Isochronous Load Sharing:** Using digital governors to ensure all parallel units share the {{cookiecutter.it_capacity_mw}} MW load precisely.
3.  **Permanent Magnet Generator (PMG):** For superior short-circuit sustainment and cleaner power to the voltage regulator (AVR).

## 6. Failure Modes & Common Mistakes
*   **Fuel Contamination:** Algae growth in diesel due to environmental humidity. *Mitigation:* Automated fuel polishing systems.
*   **Wet Stacking:** Running DGs at low load (<30%) during testing causes unburnt fuel in the exhaust. *Mitigation:* Monthly load bank testing.

## 7. Design Checklist
- [ ] Are the DGs compliant with local environmental emission norms?
- [ ] Is the "Data Centre Continuous" (DCC) rating certificate provided by the OEM?
- [ ] Is the radiator sized for {{cookiecutter.max_ambient_temp}}°C ambient to prevent "High Temp" trips?
- [ ] Are the starter batteries redundant (Dual-starter motors)?
