# Title: Lightning Protection Systems (LPS) for AI Data Centres
## Purpose: To define the design and installation criteria for a comprehensive Lightning Protection System to safeguard the facility and high-value AI equipment.
## Project: {{cookiecutter.project_name}}
## Tags: #LightningProtection #LPS #SurgeProtection #IEC62305 #RollingSphere
## Standards Covered: IEC 62305 (Parts 1-4), NFPA 780, Local Building Codes

---

## 1. Overview
A {{cookiecutter.it_capacity_mw}} MW AI data centre represents a massive investment in sensitive {{cookiecutter.ai_silicon_vendor}} GPU hardware. A single lightning strike—either a direct hit or an indirect surge (LEMP)—can cause catastrophic equipment failure. The keraunic level (thunderstorm days per year) in {{cookiecutter.city}} necessitates a robust, low-impedance LPS designed per **IEC 62305**.

## 2. Risk Assessment (IEC 62305-2)
A mandatory Risk Assessment determines the **Lightning Protection Level (LPL)**.
*   **Target for {{cookiecutter.project_name}}:** **LPL II / Class II** (due to the density and value of AI clusters; yields 95% protection efficiency).

## 3. External Lightning Protection (The Faraday Cage)
The design follows the "Rolling Sphere Method" (RSM).

### 3.1 Air Termination System
*   **Method:** A combination of vertical air terminals and a roof mesh.
*   **Height:** Determined by the rolling sphere radius (30m for Class II).
*   **Placement:** All rooftop equipment (CDUs, Chillers, DG Exhausts) must be within the "Zone of Protection."

### 3.2 Down Conductors
*   **Requirement:** Multiple paths to earth to distribute the current and reduce electromagnetic fields inside the building.
*   **Standard:** Utilize the building's structural steel reinforcement (rebar) as "Natural Down Conductors". 
*   **Spacing:** 10 meters (for Class II).

## 4. Internal Lightning Protection (Surge Protection)
External rods do not protect against surges entering via cables. Cascaded SPDs are mandatory.

| SPD Type | Location | Target |
| :--- | :--- | :--- |
| **Type 1 (Class I)** | Main HT/LT Incomers | Direct lightning current (10/350 µs wave). |
| **Type 2 (Class II)** | UPS Output / PDUs | Switching surges & indirect strikes (8/20 µs wave). |
| **Type 3 (Class III)** | AI Racks / Networking | Sensitive electronics protection (point-of-use). |

## 5. Engineering Calculations: Separation Distance ($s$)
To prevent "Side-Flashing" between the LPS and internal electrical systems.
*   **Formula:** $s = k_i \cdot \frac{k_c}{k_m} \cdot l$
*   **Design Rule:** If $s >$ actual distance, equipotential bonding is required.

## 6. AI-Ready Design Considerations
1.  **Liquid Cooling CDU Protection:** Liquid cooling systems involve massive rooftop infrastructure. These MUST be bonded to the LPS to prevent surges from traveling through pipes into the AI racks.
2.  **Fiber Optic Isolation:** The **metallic armor** in Outside Plant (OSP) fiber can carry lightning currents. Ensure all fiber shields are grounded at the building entry.

## 7. Failure Modes
*   **Side-Flashing:** Lightning jumping from a down conductor into an internal power cable. *Mitigation:* Proper separation distance.
*   **SPD Failure:** Repeated surges wear out the MOV. *Mitigation:* SPDs with remote BMS alarm contacts.

## 8. Design Checklist
- [ ] Has an IEC 62305-2 Risk Assessment been documented for {{cookiecutter.city}}?
- [ ] Are all rooftop CDUs and Chillers within the Rolling Sphere zone?
- [ ] Are Type 1 SPDs installed at the Main LT Incomer?
