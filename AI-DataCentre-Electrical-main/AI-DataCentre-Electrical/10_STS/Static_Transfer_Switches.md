# Title: Static Transfer Switches (STS) - High-Speed Power Path Redundancy
## Purpose: To define the technical specifications, application logic, and selection criteria for high-speed Static Transfer Switches in the {{cookiecutter.project_name}} facility.
## Tags: #STS #StaticTransferSwitch #Redundancy #HighSpeedSwitching #Thyristor
## Standards Covered: IEC 62310-1/2/3, IEEE 446, IEEE 3001.2

---

## 1. Overview
In a {{cookiecutter.it_capacity_mw}} MW AI-ready facility, the Static Transfer Switch (STS) is a critical solid-state device used to switch power between two independent, synchronized AC sources (usually UPS A and UPS B). Unlike an Automatic Transfer Switch (ATS) which uses mechanical contactors and takes 20-50ms, an STS uses SCRs (Silicon Controlled Rectifiers) to achieve transfers in **< 4ms (1/4 of a cycle)**, ensuring that sensitive {{cookiecutter.ai_silicon_vendor}} servers and network switches do not reboot during a power path failure.

## 2. Theory: The Physics of High-Speed Switching
An STS operates on the principle of **"Break-before-Make"** using Thyristors (SCRs).
*   **Transfer Window:** Most IT power supplies (SMPS) have a hold-up time of 10-20ms (as per ITIC/CBEMA curves). The STS's 4ms transfer time is well within this window, making the transition "invisible" to the load.

## 3. Design Philosophy: Where to place the STS?
### 3.1 Primary STS (System Level)
*   **Placement:** Between Main UPS Distribution Boards.
*   **Capacity:** 800A to 2000A.
*   **Use Case:** Providing a redundant path to a large block of PDUs or Busways.

### 3.2 Secondary STS (Rack/PDU Level)
*   **Placement:** Within the IT Rack or PDU.
*   **Capacity:** 16A to 63A (Rack-mount) or 100A-400A (PDU-mount).
*   **Use Case:** Supporting single-corded devices (e.g., legacy network gear or specific liquid cooling pumps) within a dual-path architecture.

## 4. Engineering Calculations
### 4.1 Short Circuit Withstand
Since an STS is a semiconductor device, it is extremely sensitive to faults.
*   **Formula:** $I^2t$ (Amperes squared x Time).
*   **Requirement:** The STS must be rated to withstand the downstream fault level until the branch circuit breaker clears. 
*   **Worked Example:** If a branch circuit fault is 10kA and the breaker clears in 10ms, the STS SCRs must have an $I^2t$ rating higher than $(10,000^2 \times 0.01) = 1,000,000 A^2s$.

### 4.2 Heat Dissipation
STS units generate heat due to the forward voltage drop across the SCRs.
*   **Calculation:** ~1% of the rated kW is dissipated as heat. Ensure the electrical room HVAC in {{cookiecutter.city}} can handle this localized heat rejection.

## 5. AI-Ready Integration
*   **Inrush Current Handling:** When an STS transfers power to an {{cookiecutter.ai_silicon_vendor}} rack cluster, the combined inrush of the transformers/capacitors can be massive. The STS must have **"Soft-Transfer"** logic or be significantly oversized (e.g., 1000% overload for 1 cycle).
*   **Phase Sync Monitoring:** The STS must inhibit a transfer if the sources are out of sync (>15 degrees) to prevent high circulating currents.

## 6. Failure Modes
*   **SCR Short Circuit:** If one SCR shorts, it may connect Source 1 and Source 2 together. *Mitigation:* Use high-speed internal fuses.
*   **Control Logic Freeze:** The STS fails to transfer. *Mitigation:* Use redundant power supplies and logic boards.

## 7. Design Checklist
- [ ] Are Source 1 and Source 2 synchronized? (Check UPS Sync Bus).
- [ ] Is the STS $I^2t$ rating coordinated with the downstream breaker clearing time?
- [ ] Does the STS have a manual maintenance bypass?
- [ ] For 4-pole units, is the neutral switching "Make-before-Break" to avoid floating neutrals?
