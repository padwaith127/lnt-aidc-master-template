# Title: IEC Standards for Electrical Equipment & Assemblies
## Purpose: To define the International Electrotechnical Commission (IEC) standards required for equipment specification and testing in a 40 MW facility.
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #IEC #Switchgear #Transformers #Safety #Testing #LTVyoma
## Related Files: [[BIS.md]], [[LV_Switchgear.md]], [[Transformer_Design.md]], [[Busbar_Distribution.md]]
## Standards Covered: IEC 61439, IEC 60076, IEC 62271, IEC 60364, IEC 62040

---

## 1. Overview
While IEEE governs the *analysis* of the system, **IEC (International Electrotechnical Commission)** standards govern the *hardware*. For the L&T Mahape project, all procurement from vendors (ABB, Schneider, Siemens) must be compliant with the latest IEC editions. This ensures the 40 MW facility is built with components that are safe, interoperable, and tested.

## 2. Core IEC Standards for Data Centre Hardware

### 2.1 LV Switchgear: IEC 61439-1 & 2
*   **Significance:** Replaced the old IEC 60439. It defines the "Assembly" rather than just the components.
*   **Requirement:** All PCCs and MCCs must be **Type Tested** (TTA) as a complete assembly.
*   **Mahape Application:** Specify **Form 4b** separation as per Part 2 of this standard.

### 2.2 HT Switchgear: IEC 62271 Series
*   **Significance:** Governing High-Voltage (HT) switchgear and controlgear.
*   **Part 200:** AC metal-enclosed switchgear for voltages > 1 kV up to 52 kV.
*   **Part 100:** High-voltage alternating current circuit-breakers.

### 2.3 Transformers: IEC 60076
*   **Significance:** The global benchmark for Power and Distribution Transformers.
*   **Data Centre Context:** Focus on **Part 11** for Dry-type (Cast Resin) transformers and **Part 1** for oil-filled HT transformers.

### 2.4 Low Voltage Installations: IEC 60364
*   **Significance:** The global "Electrical Code" that mirrors the US NEC.
*   **Data Centre Context:** **Section 8-1** covers Energy Efficiency (PUE/pPUE optimization).

### 2.5 UPS Systems: IEC 62040-3
*   **Significance:** Defines the method of specifying the performance and test requirements of UPS units.
*   **Classification:** For Mahape, specify **VFI-SS-111** (Voltage and Frequency Independent, Sinusoidal output).

## 3. Mandatory Testing (IEC Requirements)
As an L&T PM, you must witness "Routine Tests" based on these IEC standards:
1.  **Dielectric Tests:** To check insulation integrity.
2.  **Temperature Rise Tests:** To ensure the 4000A busbar doesn't overheat.
3.  **Short-time Withstand:** To prove the busbar supports can handle the 65kA mechanical kick.

## 4. IEC vs. IS Standards (The Indian Context)
In many cases, Indian Standards (BIS) have adopted IEC standards (e.g., IS/IEC 62305 for Lightning). Where an IS exists, it must be followed for local statutory compliance; where it doesn't, the IEC is the default global authority for L&T.

## 5. Design Checklist (IEC Compliance)
- [ ] Are all LV panels certified to IEC 61439-1 & 2?
- [ ] Are the transformers tested per IEC 60076?
- [ ] Is the HT switchgear (VCB/GIS) rated and tested per IEC 62271-100/200?
- [ ] Are UPS units classified as VFI-SS-111 per IEC 62040-3?
- [ ] Is the IP (Ingress Protection) rating for outdoor gear IP55/65 per IEC 60529?

---

## 6. References
### Standards
* **IEC 61439:** Low-voltage switchgear and controlgear assemblies.
* **IEC 62271:** High-voltage switchgear and controlgear.
* **IEC 60076:** Power transformers.

### Revision History
* 1.0: Mapped core IEC standards for L&T Vyoma Mahape project.