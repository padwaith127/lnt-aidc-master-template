# Title: Busbar Distribution Systems (Main & Track Busway)
## Purpose: To define the engineering specifications for high-ampacity power distribution (2500A - 6000A) in the {{cookiecutter.project_name}}.
## Tags: #Busduct #Busway #PowerDistribution #TrackBusway #AI-Infrastructure
## Standards Covered: IEC 61439-6, IEEE C37.23, UL 857

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW hyperscale facility, traditional cabling is physically impossible for main power backbones. To move massive power from transformers to the AI data halls, we utilize **Sandwich Busducts** (Main) and **Open-Channel Track Busways** (Rack-level). 

## 2. Busduct Technology Selection

| Feature | Sandwich Busduct (Main) | Open-Channel Track Busway (Rack) |
| :--- | :--- | :--- |
| **Typical Rating** | 2500A to 6000A+ | 400A to 1200A |
| **Application** | Transformer to LV Panel; UPS to PDU | Overhead distribution in Data Halls |
| **Flexibility** | Fixed joints (Rigid) | Plug-in units anywhere along the run |
| **Insulation** | Mylar/Epoxy (Class F/H) | Air-insulated with copper busbars |

## 3. Engineering Calculations
### 3.1 Sizing based on Continuous Current
Current ($I$) must be calculated at the derated ambient temperature ({{cookiecutter.max_ambient_temp}}°C for {{cookiecutter.city}}).
*   **Formula:** $I_{design} = \frac{S_{kva} \times 1000}{\sqrt{3} \times V} \times K_{df}$
*   **Constraint:** Apply a 1.25 multiplier for continuous AI loads (NEC/Local Codes).

### 3.2 Short-Circuit Withstand ($I_{cw}$)
*   **Design Basis:** Must withstand the {{cookiecutter.fault_level_ka}} kA fault level defined in the Short Circuit Study for 1 Second.
*   **Force:** Mechanical force $F \propto \frac{I^2}{d}$. Sandwich design minimizes this force.

### 3.3 Voltage Drop Calculation
*   **Formula:** $\Delta V = \sqrt{3} \times I \times (R \cos \phi + X \sin \phi) \times L$
*   **Constraint:** Maintain $< 2\%$ drop on the main distribution runs.

## 4. AI-Ready Design Features
1.  **200% Neutral Sizing:** Mandatory for AI zones to handle additive 3rd harmonic currents from thousands of single-phase GPU power supplies.
2.  **Harmonic Derating:** High-frequency components of AI loads increase the "Skin Effect." Ensure the manufacturer has tested the busduct with a high **K-factor** load profile.
3.  **Integral Earth:** Use the housing as an earth plus an internal dedicated copper earth bar for the "Clean Earth" (SRG) required by {{cookiecutter.ai_silicon_vendor}} networking.

## 5. Construction & Layout 
*   **Seismic Bracing:** Use rigid bracing and "Flexible Links" (Braided/Laminated) at transformer connections and across building expansion joints based on the {{cookiecutter.city}} seismic zone.
*   **Fire Barriers:** Internal and external **Fire Stops** (2-hour or 4-hour rated) must be installed at all fire-wall penetrations.

## 6. Failure Modes
*   **Thermal Expansion Stress:** Failure to use "Expansion Bellows" on long runs leads to joint cracking.
*   **Loose Bolts:** Leads to "Hot Spots" and eventual arc flash. *Mitigation:* Torque shear-bolts correctly and mandate bi-annual Infrared (IR) scanning.

## 7. Design Checklist
- [ ] Is the busbar material 99.9% ETP Grade Copper or tested Aluminum alloy?
- [ ] Has a 200% Neutral been specified for the IT Data Hall runs?
- [ ] Are flexible links provided at the Transformer/Switchgear interface?
- [ ] Has the voltage drop been verified for the longest run at 100% load?
