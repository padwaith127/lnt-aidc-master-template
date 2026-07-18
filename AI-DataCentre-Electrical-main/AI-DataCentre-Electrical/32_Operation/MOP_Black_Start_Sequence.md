# Title: MOP: 40MW Facility Black Start Sequence
## Purpose: Step-by-step restoration of power from a total site blackout.
## Revision: 1.0
## Date: 24-May-2024
## Tags: #BlackStart #OperationalContinuity #MOP #LTVyoma
## Related Files: [[Backup_Generation.md]], [[SCADA.md]]

---

## 1. Initial State
*   Utility Power: LOST.
*   UPS: On Battery (Remaining runtime < 10 mins).
*   Generators: Initiating Auto-Start.

## 2. Restoration Steps
1.  **DG Synchronization:** Verify all 20+ DG units reach 50Hz/11kV and sync to the common bus.
2.  **Critical Cooling (Step 1):** Close breakers for Primary Pumps and CDUs (Liquid Cooling). **Mandatory:** Liquid flow must be restored before UPS batteries expire.
3.  **Mechanical Plant (Step 2):** Sequence-start Chillers at 10-second intervals to prevent voltage dips.
4.  **IT Re-Load:** Verify UPS is back in "Normal Mode" (Rectifier taking load).

## 3. Emergency Actions
*   If DG-1 fails to sync, the SCADA must initiate "Load Shedding" of non-critical lighting and administrative loads immediately.

---
## 📚 References
* **Cummins:** Paralleling & Synchronization Guide.
* **Uptime:** Operational Sustainability Standard.