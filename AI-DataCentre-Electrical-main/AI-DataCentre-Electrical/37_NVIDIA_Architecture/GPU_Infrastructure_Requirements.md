# Title: NVIDIA GPU Infrastructure - Electrical Power Requirements
## Purpose: To define the specific electrical infrastructure, power profiles, and deployment requirements for NVIDIA AI clusters (H100, B200, GB200).
## Revision: 1.0
## Date: 24-May-2024
## Version: 1.0
## Tags: #NVIDIA #H100 #Blackwell #GB200 #StepLoad #GPUInfrastructure #LTVyoma
## Related Files: [[AI_Load_Estimation.md]], [[High_Density_Thermal_Management.md]], [[Rack_Level_Distribution.md]]
## Standards Covered: NVIDIA Gold Site Survey Requirements, OCP ORV3, IEEE 1100, IEC 62368-1

---

## 1. Overview
In the L&T Mahape 40 MW project, the electrical design is purpose-built to host NVIDIA GPU infrastructure. Unlike standard CPU-based servers, NVIDIA AI clusters (specifically the Blackwell/GB200 architecture) exhibit extreme power density and highly dynamic load profiles. This module provides the technical "specs" for the electrical engineer to ensure the infrastructure is "NVIDIA-Certified."

## 2. NVIDIA Deployment Architectures

| Architecture | Description | Typical Power per Rack | Cooling |
| :--- | :--- | :--- | :--- |
| **HGX / DGX H100** | Standard 8-GPU Baseboards. | 15 kW - 40 kW | Air or Liquid (D2C) |
| **Blackwell HGX B200** | Next-gen high-performance cluster. | 60 kW - 100 kW | Liquid (Mandatory) |
| **GB200 NVL72** | Liquid-cooled rack with 72 GPUs as one unit. | 120 kW+ | Liquid (D2C) |

## 3. Power Step-Load & Transient Profiles
AI training is characterized by "Bursty" compute cycles.
1.  **Training Initialization:** Power jumps from 10% to 80% in < 50ms.
2.  **Checkpointing:** Sudden drop in power as data is written to disk.
3.  **Communication Phase:** Fluctuating power draw as GPUs exchange data via NVLink.

**L&T Engineering Mandate:** 
The UPS and Generator systems must handle a **di/dt of >100A per millisecond** at the rack level without the voltage dropping below the ITIC lower bound (typically -10% of nominal).

## 4. Engineering Calculations: TDP vs. Peak Power

### 4.1 Thermal Design Power (TDP)
TDP represents the continuous power draw.
*   **H100 GPU:** ~700W per GPU.
*   **B200 GPU:** ~1000W to 1200W per GPU.

### 4.2 Peak Power Requirement
NVIDIA recommends sizing electrical circuits for the **Maximum Peak Power**, which includes the GPU, CPU, Fans, and Power Shelf losses.
*   **Formula:** $P_{total} = (N_{gpu} \times P_{gpu\_peak}) + (N_{cpu} \times P_{cpu}) + P_{fans} + P_{loss}$
*   **Example (GB200 NVL72):**
    *   72 GPUs @ 1200W = 86.4 kW.
    *   Compute Tray CPUs + Networking = ~20 kW.
    *   Liquid Cooling Pumps/Internal Fans = ~5 kW.
    *   **Total Rack TDP:** ~111.4 kW.
    *   **Design Overhead (10%):** ~122.5 kW.
    *   **Selection:** 130 kVA Power Path.

## 5. The 48V DC Ecosystem
NVIDIA Blackwell systems utilize the **OCP Open Rack V3 (ORV3)** power architecture.
*   **Input:** 415V, 3-Phase AC into the Power Shelf.
*   **Output:** 48V DC (nominal) to the server backplane.
*   **Why?** To handle the 2,500A currents required for 120kW compute without melting cables.
*   **Grounding:** The 48V DC return is typically referenced to the rack frame at a single point to prevent ground loops.

## 6. AI-Ready Networking Power (The "Third Network")
NVIDIA clusters require three distinct networks, each with its own power impact:
1.  **Compute Fabric (InfiniBand/Spectrum-X):** High-speed interconnects between GPUs. High power draw at the switch level.
2.  **Storage Fabric:** High-speed data feed.
3.  **Management Network:** Low speed (SOP/EOP).

**L&T Strategy:** Ensure that "Networking Racks" (Switch Racks) are not under-sized. An InfiniBand switch rack for a large cluster can draw **20kW to 30kW** on its own.

## 7. AI Site Survey Checklist (The NVIDIA Requirements)

| Parameter | Requirement | L&T Mahape Implementation |
| :--- | :--- | :--- |
| **Voltage Tolerance** | +/- 5% Steady State | UPS Bypass & Rectifier Settings. |
| **Frequency Tolerance** | +/- 0.5 Hz | DG Isochronous Governors. |
| **THDv** | < 3% | Active Harmonic Filtering. |
| **Neutral-to-Earth** | < 1.0 V | Dedicated Signal Reference Grid. |
| **DC Busbar Ripple** | < 1% | High-capacitance Power Shelves. |

## 8. Construction & Deployment (L&T Execution)
*   **Busway Tap-offs:** Use "Heavy Duty" tap-off boxes (250A/400A) with integrated energy metering.
*   **Fiber Protection:** AI clusters involve thousands of fibers. Ensure electrical cable trays do not overlap or crush high-density fiber troughs (e.g., Panduit FiberRunner).
*   **Weight Management:** Ensure the raised floor (if used) or concrete slab is reinforced for the **1.5 to 2.5 metric ton** weight of an NVIDIA NVL72 rack.

## 9. Commissioning & Readiness
1.  **Load Step Simulation:** Use Load Banks that can trigger 0-100% steps to test the UPS and DG response.
2.  **Harmonic Audit:** Confirm that the NVIDIA rectifiers are not creating resonance with the facility's power factor correction (PFC) banks.
3.  **Redundancy Test:** Pull "Source A" and verify the Blackwell power shelf handles the load on "Source B" without any GPU performance throttling.

## 10. Failure Modes
*   **Current Overloading:** During "Maximum Compute," a poorly balanced rack can trip one phase of a 3-phase input.
*   **Transient Voltage Swell:** When an AI job finishes, the sudden 100kW load drop can cause a voltage swell that affects neighboring sensitive hardware.
*   **Thermal Trip:** Failure of the CDU pump (Electrical issue) leads to GPU shutdown in < 15 seconds.

---

## 11. Design Checklist
- [ ] Is the design capable of 120kW per rack?
- [ ] Does the UPS handle a 100% load step within 1 cycle?
- [ ] Is the Signal Reference Grid (SRG) connected to every NVIDIA rack?
- [ ] Are the busway tap-offs rated for continuous operation at 50°C?
- [ ] Has the InfiniBand networking switch power been accounted for?

---
## 12. References
### Standards
* **NVIDIA DGX/HGX Site Preparation Guide:** (Proprietary/Partner Access).
* **OCP Open Rack V3 (ORV3):** Power and Infrastructure Specifications.
* **IEEE 1100:** Recommended Practice for Powering and Grounding (Emerald Book).

### Research Papers
* **NVIDIA White Paper:** "Accelerating AI with Blackwell Architecture."
* **Uptime Institute:** "Infrastructure Requirements for High-Density AI Racks."

### Revision History
* 1.0: Initial NVIDIA Architecture spec for L&T Vyoma Mahape.

---
**Next File Recommendation:** `38_Drawings/Standard_Drawing_Templates.md` (Defining how to create the SLDs, Layouts, and Protection drawings for the 40 MW facility).