# Title: Static Transfer Switches (STS) - High-Speed Power Path Redundancy
## Purpose: To define the technical specifications, application logic, and selection criteria for high-speed Static Transfer Switches in a 40 MW AI-ready facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #STS #StaticTransferSwitch #Redundancy #PowerPath #HighSpeedSwitching #Thyristor #Availability
## Related Files: [[UPS_System_Design.md]], [[LV_Switchgear.md]], [[Rack_Power.md]]
## Standards Covered: IEC 62310-1/2/3, IEEE 446, IEEE 3001.2

---

## 1. Overview
In a 40 MW AI-ready facility, the Static Transfer Switch (STS) is a critical solid-state device used to switch power between two independent, synchronized AC sources (usually UPS A and UPS B). Unlike an Automatic Transfer Switch (ATS) which uses mechanical contactors and takes 20-50ms, an STS uses SCRs (Silicon Controlled Rectifiers) to achieve transfers in **< 4ms (1/4 of a cycle)**, ensuring that sensitive AI servers and network switches do not reboot during a power path failure.

## 2. Theory: The Physics of High-Speed Switching
An STS operates on the principle of **"Break-before-Make"** using Thyristors (SCRs).
*   **Thyristor Operation:** SCRs act as high-speed electronic valves. By controlling the "Gate" pulse, the STS can stop the current flow from Source 1 and initiate it from Source 2 almost instantaneously.
*   **Transfer Window:** Most IT power supplies (SMPS) have a hold-up time of 10-20ms (as per ITIC/CBEMA curves). The STS's 4ms transfer time is well within this window, making the transition "invisible" to the load.

## 3. Design Philosophy: Where to place the STS?

### 3.1 Primary STS (System Level)
*   **Placement:** Between Main UPS Distribution Boards.
*   **Capacity:** 800A to 2000A.
*   **Use Case:** Providing a redundant path to a large block of PDUs or Racks.

### 3.2 Secondary STS (Rack/PDU Level)
*   **Placement:** Within the IT Rack or PDU.
*   **Capacity:** 16A to 63A (Rack-mount) or 100A-400A (PDU-mount).
*   **Use Case:** Supporting single-corded devices (e.g., legacy network gear or specific liquid cooling pumps) within a dual-path architecture.

## 4. Engineering Calculations

### 4.1 Short Circuit Withstand
Since an STS is a semiconductor device, it is more sensitive to faults than a breaker.
*   **Formula:** $I^2t$ (Amperes squared x Time).
*   **Requirement:** The STS must be rated to withstand the downstream fault level until the branch circuit breaker clears. 
*   **Worked Example:** If a branch circuit fault is 10kA and the breaker clears in 10ms, the STS SCRs must have an $I^2t$ rating higher than $(10,000^2 \times 0.01) = 1,000,000 A^2s$.

### 4.2 Heat Dissipation
STS units generate heat due to the forward voltage drop across the SCRs.
*   **Typical Efficiency:** 99%.
*   **Calculation:** 1% of the rated kW is dissipated as heat.
*   **Example:** A 1000A STS at 415V ($P \approx 700 kW$) will dissipate ~7kW of heat. This must be accounted for in the Electrical Room cooling design.

## 5. Equipment Selection Criteria

| Feature | Requirement | Reasoning |
| :--- | :--- | :--- |
| **Transfer Time** | ≤ 4 ms | Ensures IT power supplies don't drop. |
| **Number of Poles** | 3-Pole or 4-Pole | 4-Pole is required if the sources have different neutral references. |
| **Overload Capacity** | 125% for 10 mins / 1000% for 1 cycle | Must handle inrush currents from AI power shelves. |
| **Control Logic** | Dual redundant controllers | Prevents STS failure if one control board dies. |
| **Maintenance** | Integrated Bypass | Allows servicing of SCRs without dropping the load. |

## 6. AI-Ready Integration
*   **Inrush Current Handling:** When an STS transfers power to an AI rack cluster, the combined inrush of the transformers/capacitors in the power shelves can be massive. The STS must have **"Soft-Transfer"** logic or be significantly oversized.
*   **Phase Sync Monitoring:** The STS must monitor the phase angle between Source 1 and Source 2. It should inhibit a transfer if the sources are out of sync (>15 degrees) to prevent high circulating currents and potential transformer saturation.

## 7. Commissioning & Testing (Level 4/5)
1.  **Transfer Test (Normal):** Manually initiate a transfer and observe the waveform on a power quality analyzer (Swell/Dip check).
2.  **Failure Transfer Test:** Simulate the loss of Source 1 (by pulling the breaker) and verify automatic transfer to Source 2.
3.  **Out-of-Phase Test:** Verify the STS "Inhibit" function works when sources are unsynchronized.
4.  **Short Circuit Simulation:** Verify the STS survives a downstream fuse/breaker clearing event.

## 8. Failure Modes
*   **SCR Short Circuit:** If one SCR shorts, it may connect Source 1 and Source 2 together. *Mitigation:* Use high-speed internal fuses and an "Isolation Transformer" if neutral isolation is needed.
*   **Control Logic Freeze:** The STS fails to transfer. *Mitigation:* Use redundant power supplies and logic boards.
*   **Overheating:** Blocked air filters in the STS cabinet. *Mitigation:* Temperature sensors and BMS alarms.

## 9. Design Checklist
- [ ] Are Source 1 and Source 2 synchronized? (Check UPS Sync Bus).
- [ ] Is the STS $I^2t$ rating coordinated with the downstream breaker clearing time?
- [ ] Does the STS have a manual maintenance bypass?
- [ ] Is the STS communicating with the EPMS/SCADA via Modbus/TCP or SNMP?
- [ ] For 4-pole units, is the neutral switching "Make-before-Break" to avoid floating neutrals?

---
## 📚 References
### Standards
* **IEC 62310-1:** Static transfer systems (STS) - General and safety requirements.
* **IEC 62310-2:** STS - Electromagnetic compatibility (EMC) requirements.
* **IEC 62310-3:** STS - Method for specifying performance and test requirements.

### Manufacturer Documents
* **Schneider Electric:** "APC Silcon STS Technical Guide."
* **Vertiv:** "Liebert STS2 Static Transfer Switch Data Sheet."
* **ABB:** "Cyberex SuperSwitch 4 Digital Static Transfer Switch."

### Revision History
* 1.0: Initial setup for L&T Vyoma Mahape project high-speed switching strategy.

---
**Next File Recommendation:** `13_PDU/Power_Distribution_Units.md` (Focusing on the final distribution step before the AI Racks).