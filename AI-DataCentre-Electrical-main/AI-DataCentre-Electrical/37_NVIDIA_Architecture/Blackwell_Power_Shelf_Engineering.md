# Title: NVIDIA Blackwell (GB200) Power Shelf & DC Busbar Engineering
## Purpose: Detailed electrical design for the 120kW AI Power Shelf and 48V DC distribution.
## Revision: 1.0
## Date: 24-May-2024
## Tags: #Blackwell #GB200 #48VDC #PowerShelf #NVIDIA
## Standards: OCP ORV3, IEC 62368-1

---

## 1. Input Requirements
*   **Voltage:** 415V 3-Phase AC, 50Hz.
*   **Feeds:** Dual 63A or 125A feeds (Source A & B) via IEC 60309 Pin-and-Sleeve connectors.

## 2. Rectification & Conversion
*   **Topology:** N+1 or N+N (Shelf contains 6-12 hot-swappable rectifier modules).
*   **Output:** 48V DC nominal (Range 44V-54V).
*   **Efficiency:** >97.5% (Titanium Grade).

## 3. DC Busbar Design (The "Backplane")
*   **Current:** ~2,500 Amperes per rack.
*   **Material:** Copper with Silver/Tin plating.
*   **Cooling:** Primarily Air-cooled within the shelf; GPUs are liquid-cooled.

## 4. Protection & Selectivity
*   **AC Side:** Branch circuit breakers at the Busway tap-off.
*   **DC Side:** High-speed e-Fuses (Electronic Fuses) at each GPU node to prevent "Busbar Vaporization" during a DC short circuit.

---
## 📚 References
* **NVIDIA:** Blackwell Infrastructure Design Guide.
* **OCP:** Open Rack V3 Power Specifications.