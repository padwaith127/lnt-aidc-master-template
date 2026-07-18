# Title: Busbar Distribution Systems (Main & Track Busway)
## Purpose: To define the engineering specifications for high-ampacity power distribution (2500A - 6000A) in a 40 MW AI-ready hyperscale facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #Busduct #Busway #PowerDistribution #HighAmpacity #SandwichBusduct #TrackBusway #AI-Infrastructure
## Related Files: [[Transformer_Design.md]], [[UPS_System_Design.md]], [[Rack_Power.md]], [[Voltage_Drop.md]]
## Standards Covered: IEC 61439-6, IEEE C37.23, IS 8623, UL 857, NBC 2016

---

## 1. Overview
In a 40 MW hyperscale facility, traditional cabling is physically impossible for main power backbones. To move 55+ MVA from transformers to the UPS rooms and then to the AI data halls, we utilize **Sandwich Busducts** (Main) and **Open-Channel Track Busways** (Rack-level). 

For the L&T Mahape project, the busduct system must handle high short-circuit forces and manage the thermal stress induced by non-linear AI loads.

## 2. Busduct Technology Selection

| Feature | Sandwich Busduct (Main) | Open-Channel Track Busway (Rack) |
| :--- | :--- | :--- |
| **Typical Rating** | 2500A to 6300A | 400A to 1200A |
| **Application** | Transformer to LV Panel; UPS to PDU | Overhead distribution in Data Halls |
| **Flexibility** | Fixed joints (Rigid) | Plug-in units anywhere along the run |
| **Insulation** | Mylar/Epoxy (Class F/H) | Air-insulated with copper busbars |
| **Ingress Protection** | IP54 to IP66 | IP2X to IP3X |

## 3. Engineering Calculations

### 3.1 Sizing based on Continuous Current
Current ($I$) must be calculated at the derated ambient temperature (50°C for Mahape).
*   **Formula:** $I_{design} = \frac{S_{kva} \times 1000}{\sqrt{3} \times V} \times K_{df}$
    *   $S_{kva}$: 2500 kVA (Typical Transformer)
    *   $V$: 415 V
    *   $K_{df}$: Derating factor for 50°C ambient (typically 0.8 to 0.9).
*   **Worked Example:**
    $I_{load} = \frac{2500 \times 1000}{1.732 \times 415} \approx 3478 \text{ A}$
    Applying 1.25 factor for continuous AI load (NEC/CEA): $3478 \times 1.25 \approx 4347 \text{ A}$.
    **Selection:** **5000A Copper Sandwich Busduct**.

### 3.2 Short-Circuit Withstand ($I_{cw}$)
The busduct must withstand the mechanical forces of a fault without deforming.
*   **Design Basis:** 50kA or 65kA for 1 Second (matching the LV Switchgear).
*   **Force Calculation (Simplified):** Mechanical force $F \propto \frac{I^2}{d}$ (where $d$ is distance between bars). Sandwich design minimizes this force by reducing $d$.

### 3.3 Voltage Drop Calculation
Critical for long runs (e.g., from an external HT yard to an internal UPS room).
*   **Formula:** $\Delta V = \sqrt{3} \times I \times (R \cos \phi + X \sin \phi) \times L$
*   **Constraint:** Maintain $< 2\%$ drop on the main distribution run.

## 4. AI-Ready Design Features
1.  **200% Neutral Sizing:** Mandatory for AI zones to handle additive 3rd harmonic currents from thousands of single-phase GPU power supplies.
2.  **Harmonic Derating:** High-frequency components of AI loads increase the "Skin Effect." Ensure the manufacturer has tested the busduct with a high **K-factor** load profile.
3.  **Integral Earth (Housing):** Use the aluminum housing as an earth (minimum 50% capacity) plus an internal dedicated copper earth bar (50%) for the "Clean Earth" required by NVIDIA racks.

## 5. Construction & Layout (L&T Standards)
*   **Seismic Bracing:** Mahape is Zone III. Use rigid bracing and "Flexible Links" (Braided/Laminated) at every transformer connection and across building expansion joints.
*   **Fire Barriers:** Every time a busduct passes through a fire-rated wall (Data Hall to Corridor), an internal and external **Fire Stop** (2-hour or 4-hour rated) must be installed.
*   **Clearance:** Maintain 150mm - 300mm clearance from other services (Chilled water pipes, cable trays) to allow for heat dissipation.

## 6. Installation & Commissioning
1.  **Phasing Check:** Ensure R-Y-B-N-E orientation is consistent before bolting.
2.  **Torque Control:** Use "Double-Headed Shear Bolts" to ensure the correct torque (typically 80-120 Nm) is applied to joints.
3.  **Insulation Resistance (IR):** Minimum 100 MΩ before energization.
4.  **Contact Resistance (Ductor Test):** Measure across every joint. Resistance must be consistent across all phases and within manufacturer limits (typically < 10 micro-ohms).

## 7. Failure Modes
*   **Thermal Expansion Stress:** Failure to use "Expansion Bellows" on long runs leads to joint cracking.
*   **Water Ingress:** Leakage from overhead chilled water pipes (if not isolated). *Mitigation:* Use IP66 rated busduct in mechanical rooms and drip trays.
*   **Loose Bolts:** Leads to "Hot Spots" and eventual arc flash. *Mitigation:* Thermal imaging (Infrared) scans every 6 months.

---

## 8. Design Checklist
- [ ] Is the busbar material 99.9% ETP Grade Copper?
- [ ] Has a 200% Neutral been specified for the IT Data Hall runs?
- [ ] Are flexible links provided at the Transformer/Switchgear interface?
- [ ] Are the busduct runs coordinated with the HVAC ducting to avoid physical clashes?
- [ ] Has the voltage drop been verified for the longest run at 100% load?

---
## 📚 References
### Standards
* **IEC 61439-6:** Low-voltage switchgear and controlgear assemblies – Part 6: Busbar trunking systems.
* **IS 8623:** Specification for Low-Voltage Switchgear and Controlgear Assemblies.
* **UL 857:** Standard for Safety for Busways.

### Manufacturer Documents
* **Schneider Electric:** "Canalis High Power Busbar Technical Guide."
* **Legrand:** "Zucchini Busbar Trunking Systems Design Manual."
* **Starline:** "Track Busway System for Data Centers."

### Revision History
* 1.0: Initial release for Mahape 40MW Busbar Distribution strategy.

---
**Next File Recommendation:** `11_Switchgear/LV_Switchgear.md` (Focusing on Main LT Panels, PCCs, and MCCs).