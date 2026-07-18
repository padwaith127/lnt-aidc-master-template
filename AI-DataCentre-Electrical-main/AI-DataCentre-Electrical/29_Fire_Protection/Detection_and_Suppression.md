# Title: Fire Detection & Suppression Systems for AI Data Centres
## Purpose: To define the engineering requirements for life safety, early-warning detection, and gaseous suppression systems tailored for high-value AI GPU infrastructure.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #FireProtection #VESDA #CleanAgent #Novec1230 #FireAlarm #Hyperscale #LTVyoma
## Related Files: [[BMS_Integration.md]], [[Battery_Energy_Storage.md]], [[LV_Switchgear.md]]
## Standards Covered: NFPA 72, NFPA 75, NFPA 76, NFPA 2001, NBC 2016 (Part 4), IS 2189

---

## 1. Overview
In a 40 MW AI facility, the concentration of value is unprecedented. A single NVIDIA Blackwell rack can cost upwards of $3M. Traditional fire protection (water-based sprinklers) is a "last resort" that often causes as much damage to electronics as the fire itself. For the L&T Mahape project, we utilize a multi-layered defense strategy: **Very Early Smoke Detection (VESDA)** for warning, **Clean Agent Gaseous Suppression** for primary extinguishment, and **Double-Interlock Pre-Action Sprinklers** as a fail-safe.

## 2. Design Philosophy: The AI-Ready Fire Strategy
1.  **High Airflow Challenge:** AI racks require massive CFM. This high velocity dilutes smoke, making standard spot detectors useless.
2.  **Continuity of Service:** The system must allow for localized suppression without shutting down the entire 40 MW hall.
3.  **Non-Conductivity:** Only non-conductive, residue-free agents are permitted in the White Space.

## 3. Key Components & Selection

| System | Technology | Purpose |
| :--- | :--- | :--- |
| **Detection (Early)** | VESDA (Aspirating) | Senses products of combustion at the molecular level before visible smoke. |
| **Detection (Secondary)** | Photoelectric Spot Detectors | Cross-zoned to trigger gas release. |
| **Suppression (Gas)** | Novec 1230 / FM-200 | Chemical/Physical heat absorption; safe for electronics. |
| **Suppression (Backup)** | Pre-Action Sprinklers | Dry pipes; requires two signals (Smoke + Heat) to release water. |
| **Control** | Fire Alarm Control Panel (FACP) | The "Brain" that coordinates shutdowns and notifications. |

## 4. Engineering Calculations: Gas Concentration

### 4.1 Volume Calculation
To extinguish a fire, the gas must reach a specific "Design Concentration" (typically 4.5% to 5.8% for Novec 1230).
*   **Formula:** $W = \frac{V}{S} \times \frac{C}{100 - C}$
    *   $W$: Weight of agent (kg).
    *   $V$: Net volume of the room ($m^3$).
    *   $S$: Specific volume of the agent.
    *   $C$: Design concentration (%).
*   **Mahape Requirement:** Account for **raised floor** and **ceiling void** volumes, as smoke and gas will permeate these spaces.

### 4.2 Enclosure Integrity (Door Fan Test)
Since the gas is heavier than air, the room must be "airtight" to maintain the concentration for at least **10 minutes** (Retention Time).
*   **Action:** All cable penetrations and busduct entries must be sealed with UL-listed fire-stop materials.

## 5. AI-Ready Design Requirements
1.  **VESDA Sampling Points:** Sampling pipes must be placed at the **Return Air Grilles** of the CRAH/CRAC units or CDUs. In AI zones, this is where smoke will inevitably be pulled by high-velocity fans.
2.  **Emergency Power Off (EPO):** FACP integration must allow for selective EPO. If fire is detected in "Zone A," only "Zone A" power should be isolated to prevent site-wide AI downtime.
3.  **BESS Fire Protection (NFPA 855):** Lithium-ion battery rooms require specialized **Off-Gas Detection** to sense battery venting *before* thermal runaway occurs.

## 6. Construction & Sequence (L&T Standards)
*   **Piping:** Use Black Steel (Schedule 40) or Galvanized piping for gas distribution.
*   **Nozzles:** 360-degree or 180-degree nozzles positioned to ensure uniform distribution without obstructing airflow to AI racks.
*   **Signage:** Mandatory "Gas Released - Do Not Enter" and "Manual Release" stations at every exit.

## 7. Commissioning & Testing
1.  **Pneumatic Pipe Test:** Pressure testing the pipework at 40 psi to ensure no leaks before cylinders are connected.
2.  **Door Fan Integrity Test:** Mandatory to prove the room holds the gas concentration.
3.  **Cross-Zoning Logic:** Verify that the gas only releases when **two** independent detectors in the same zone go into alarm.
4.  **Interface Test:** Verify that on "Fire Alarm," the BMS shuts down the HVAC fans (to prevent gas dilution) and the EPMS triggers the required electrical trips.

## 8. Failure Modes
*   **False Discharge:** Caused by poor maintenance or dust during construction triggering detectors. *Mitigation:* Use "Maintenance Mode" keys during site work.
*   **Leaking Enclosure:** Gas escapes through unsealed gaps in the Mahape facility, failing to extinguish the fire. *Mitigation:* Annual integrity testing.
*   **Agent Stratification:** Gas settling at the floor and not reaching the top of a 52U AI rack. *Mitigation:* High-level and low-level nozzle placement.

---

## 9. Design Checklist
- [ ] Has a Door Fan Integrity Test been scheduled?
- [ ] Are VESDA sampling points located at the cooling return air path?
- [ ] Is the gas concentration calculated for 10-minute retention?
- [ ] Is there an Abort Switch located inside the Data Hall?
- [ ] Does the FACP have a battery backup for 24 hours (standby) + 30 mins (alarm)?

---
## 10. References
### Standards
* **NFPA 2001:** Standard on Clean Agent Fire Extinguishing Systems.
* **NFPA 75:** Standard for the Fire Protection of IT Equipment (Mandatory for AI DCs).
* **NBC 2016 (Part 4):** Fire and Life Safety (India).
* **IS 2189:** Selection, Installation, and Maintenance of Automatic Fire Detection and Alarm System.

### Manufacturer Documents
* **Honeywell / NOTIFIER:** "Data Center Fire Protection Application Guide."
* **Johnson Controls / Ansul:** "Sapphire (Novec 1230) Technical Manual."
* **Xtralis:** "VESDA Design Guide for High-Airflow Environments."

### Revision History
* 1.0: Initial Fire Protection strategy for L&T Vyoma Mahape project.

---
**Next File Recommendation:** `30_Lighting/Emergency_and_General_Lighting.md` (Focusing on the illumination requirements for 24/7 operations and life safety).