# Title: Battery Energy Storage Systems (BESS) - Lithium-ion Focus
## Purpose: To define the engineering, safety, and performance requirements for the energy storage systems supporting a 40 MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #BESS #LithiumIon #LFP #NMC #FireSafety #NFPA855 #EnergyStorage #BMS
## Related Files: [[UPS_System_Design.md]], [[Fire_Protection.md]], [[Maintenance.md]]
## Standards Covered: NFPA 855, UL 1973, UL 9540A, IEC 62619, IS 16046, CEA 2023

---

## 1. Overview
In an AI-ready facility like L&T Mahape, Battery Energy Storage Systems (BESS) are the high-speed bridge between a utility failure and Generator synchronization. Due to the extreme power density (kW/sq.ft) required for NVIDIA infrastructure, **Lithium-ion** has superseded VRLA (Lead-Acid) as the hyperscale standard.

## 2. Chemistry Selection for AI DC
While several Lithium chemistries exist, two dominate the industry. For the Mahape project, **LFP** is generally preferred for safety and cycle life.

| Feature | LFP (Lithium Iron Phosphate) | NMC (Nickel Manganese Cobalt) |
| :--- | :--- | :--- |
| **Safety** | High (High thermal runaway temp) | Moderate (Higher energy density) |
| **Cycle Life** | 3000 - 5000 cycles | 1000 - 2000 cycles |
| **Energy Density** | Lower (More cabinets required) | Higher (Saves space) |
| **Cost** | Generally lower | Higher (due to Cobalt/Nickel) |
| **Industry Trend** | Moving towards LFP for DCs | Used where space is at an absolute premium |

## 3. Engineering Calculations: Sizing the Bank

### 3.1 Discharge Calculation (C-Rate)
AI UPS systems require massive current for short durations (5-10 mins).
*   **Formula:** $I_{dc} = \frac{P_{UPS(load)}}{V_{dc(nom)} \times \eta_{inv}}$
*   **Example:** 1500 kW UPS, 480V DC Bus, 98% Inverter Efficiency.
*   $I_{dc} = \frac{1,500,000}{480 \times 0.98} \approx 3188 \text{ Amperes}$.

### 3.2 Runtime vs. End-of-Discharge Voltage (EODV)
*   **Calculation:** Ensure the battery string can maintain the $I_{dc}$ even as voltage drops to the EODV (typically ~400V for a 480V system).
*   **Selection:** For the 40 MW site, we specify batteries with a **4C or 6C discharge rating** to handle the high power-to-energy ratio.

## 4. Safety Architecture (NFPA 855 Compliance)
Lithium-ion poses a "Thermal Runaway" risk. The design at Mahape must incorporate:
1.  **UL 9540A Testing:** Ensure the battery cabinets have undergone large-scale fire testing.
2.  **BMS (Battery Management System):** 
    *   **Level 1:** Cell monitoring (Voltage/Temp).
    *   **Level 2:** Module/Rack management (Balancing/Protection).
    *   **Level 3:** System Level (Communication with UPS and EPMS).
3.  **Gas Detection:** Detection of "Off-gassing" (Hydrogen/CO) *before* thermal runaway occurs.
4.  **Fire Suppression:** 
    *   Primary: Clean Agent (Novec 1230 or FM-200) for internal cabinet faults.
    *   Secondary: Pre-action Sprinklers (Water) to cool adjacent racks if a fire spreads.

## 5. Construction & Installation (L&T Execution)
*   **Floor Loading:** Even though Li-ion is lighter than VRLA, a 40 MW battery room requires structural verification (typically 1200-1500 kg/m²).
*   **Clearance:** Maintain 3 feet (914mm) between battery groups and between walls as per **NFPA 855**.
*   **Ventilation:** Dedicated exhaust system to prevent the buildup of toxic/flammable gases during a fault.
*   **Seismic Bracing:** Mandatory for Mahape (Zone III) to prevent cabinet tip-over.

## 6. AI-Specific Integration
*   **Fast Recharging:** AI training consumes high power; the BESS must recharge quickly to 90% SOC (State of Charge) within 4-10 hours after a discharge event.
*   **Peak Shaving (Optional):** In future phases, the BESS can be used to mitigate "Demand Charges" by discharging during peak utility tariff hours.

## 7. Commissioning & Testing
*   **Capacity Test:** Perform a "Load Bank Discharge" at 100% design load.
*   **BMS Logic Verification:** Simulate over-temperature and over-voltage to ensure the DC Breaker trips.
*   **Communication Test:** Verify SOC/SOH (State of Health) data is visible on the SCADA/BMS.

## 8. Failure Modes
*   **Internal Short Circuit:** Can lead to thermal runaway. *Mitigation:* Use LFP chemistry and high-speed DC fuses.
*   **Communication Loss:** UPS loses visibility of SOC. *Mitigation:* Redundant CAN-bus/Modbus wiring.
*   **Cell Imbalance:** Leads to reduced capacity. *Mitigation:* Active cell balancing via BMS.

---

## 9. Design Checklist
- [ ] Are the batteries UL 1973 listed and UL 9540A tested?
- [ ] Is the BMS integrated into the Emergency Power Off (EPO) loop?
- [ ] Does the battery room have 2-hour fire-rated walls?
- [ ] Are DC breakers equipped with under-voltage (UV) or shunt trips?
- [ ] Has the floor loading been verified for the concentrated weight?

---
## 📚 References
### Standards
* **NFPA 855:** Standard for the Installation of Stationary Energy Storage Systems.
* **UL 9540A:** Test Method for Evaluating Thermal Runaway Fire Propagation.
* **CEA 2023:** General Safety requirements for BESS in India.
* **IEC 62619:** Safety requirements for secondary lithium cells/batteries for industrial apps.

### Manufacturer Documents
* **Samsung SDI:** "Lithium-ion Battery Rack for UPS Operations Manual."
* **LG Energy Solution:** "Data Center BESS Design Guide."
* **Vertiv:** "Lithium-Ion Battery Systems for UPS Applications."

### Revision History
* 1.0: Initial BESS strategy for 40 MW Mahape AI DC.

---
**Next File Recommendation:** `12_Busduct/Busbar_Distribution.md` (Focusing on the 4000A - 6000A distribution required to move 40 MW throughout the facility).