# General Maintenance Procedures
**Document ID:** KOC-OPS-MAINT-001
**Clearance Level: GENERAL** — Authorised for all field engineers and maintenance personnel
**Revision:** 4.2
**Last Updated:** March 2026
**Issuing Authority:** Kuwait Oil Company — Field Operations Division

---

## 1. Purpose and Scope

This document establishes standard maintenance procedures for field equipment at Kuwait Oil Company (KOC) onshore and offshore installations. It applies to all maintenance personnel, contract engineers, and field supervisors operating at KOC-managed sites. Compliance with these procedures is mandatory. Deviation without written authorisation from a Senior Operations Engineer constitutes a procedural violation and must be reported.

---

## 2. Pre-Maintenance Safety Checklist

Before any maintenance activity begins, the following checklist must be completed in full. No steps may be skipped. The checklist must be signed and retained as part of the maintenance record.

### 2.1 Permit-to-Work (PTW) System

All non-routine maintenance activities require a valid Permit to Work before work begins.

1. Identify the work scope and classify the permit type required:
   - **Cold Work Permit** — no ignition sources, low-risk mechanical work
   - **Hot Work Permit** — welding, cutting, grinding, or any activity generating sparks or heat
   - **Confined Space Entry Permit** — entry into tanks, vessels, or enclosed pipework
   - **Electrical Isolation Permit** — work on or near live electrical systems
2. Submit the PTW request to the Area Authority (Shift Supervisor or designated permit issuer) at least two hours before planned work start.
3. The Area Authority performs a site risk assessment and signs the permit.
4. The performing authority (the engineer doing the work) reviews, understands, and co-signs the permit.
5. The permit must be physically present at the work site for the entire duration of work.
6. On completion, the performing authority signs the permit closed and returns it to the Area Authority.
7. The Area Authority confirms the site is safe, signs the permit closed, and files it.

PTW records must be retained for a minimum of five years.

### 2.2 Lock-Out / Tag-Out (LOTO) Procedure

LOTO prevents accidental energisation of equipment during maintenance. This procedure is non-negotiable and applies to all energy sources: electrical, hydraulic, pneumatic, thermal, and stored mechanical energy.

**LOTO Steps:**

1. Notify all affected personnel that a shutdown and LOTO is being performed.
2. Identify all energy sources feeding the equipment using the approved isolation diagram (available from the Control Room).
3. Shut down the equipment using the normal stopping procedure.
4. Isolate each energy source at its isolation point (disconnect switch, valve, etc.).
5. Apply a personal padlock to each isolation point. Each worker must apply their own lock — never rely on another person's lock.
6. Apply a LOTO tag to each isolation point. The tag must include: worker's name, employee number, work description, and date/time applied.
7. Release or restrain all stored energy (bleed down pressure, discharge capacitors, block against gravity movement, etc.).
8. Verify isolation by attempting to start the equipment normally and confirming no response. Test instruments and test points to confirm zero energy state.
9. Begin maintenance work only after full verification.

To remove LOTO:
1. Confirm all tools, materials, and personnel are clear of the equipment.
2. Notify all affected personnel that LOTO is being removed.
3. Remove only your own padlock and tag.
4. Restore energy sources in the correct sequence per the isolation diagram.
5. Confirm equipment returns to safe operating condition.

**Warning:** Removing another person's padlock without their consent or without following emergency LOTO removal procedures (which require supervisor authorisation and written documentation) is a serious safety violation and may result in immediate suspension.

### 2.3 Personal Protective Equipment (PPE) Requirements

Minimum PPE for all field maintenance activities:

| PPE Item | Requirement |
|---|---|
| Hard hat (EN 397 rated) | Mandatory at all times in field areas |
| Safety glasses / goggles | Mandatory. Use goggles where splash risk exists |
| Fire-resistant coverall (FRC) | Mandatory — minimum FR rating CAT 2 |
| Safety boots (steel toe, antistatic) | Mandatory |
| Nitrile gloves | Mandatory for chemical or fluid contact |
| H2S personal monitor | Mandatory — must be calibrated and bump-tested daily |
| Hearing protection | Required in high-noise zones (>85 dB) |

Additional PPE may be required depending on the specific task. Refer to the task-specific risk assessment and the PTW for any additional requirements.

---

## 3. Routine Inspection Schedule

The following schedule applies to all field equipment under KOC Field Operations. Inspections must be logged in the Computerised Maintenance Management System (CMMS) within 24 hours of completion.

### 3.1 Pumps

| Inspection Type | Frequency | Key Items |
|---|---|---|
| Visual walk-around | Daily | Leaks, unusual noise, vibration, temperature, seal condition |
| Operational check | Weekly | Flow rate vs. baseline, inlet/outlet pressure, motor current draw, bearing temperature |
| Lubrication check | Monthly | Lubricant level, condition, and contamination |
| Mechanical seal inspection | Quarterly | Seal face condition, flush system functionality, leakoff rate |
| Full preventive maintenance | Annually | Impeller inspection, shaft alignment, coupling condition, full disassembly per OEM manual |

### 3.2 Valves

| Inspection Type | Frequency | Key Items |
|---|---|---|
| Visual check | Daily | External leaks, corrosion, actuator condition (for automated valves), position indicator |
| Operational test | Monthly | Full open/close cycle, torque within specification, no binding or sticking |
| Packing inspection | Quarterly | Packing gland leakoff, packing condition, stem condition |
| Non-destructive testing | Annually | Wall thickness measurement, seat and disc condition |

### 3.3 Pressure Vessels

| Inspection Type | Frequency | Key Items |
|---|---|---|
| External visual | Weekly | Corrosion, insulation damage, nameplate legibility, vent and drain condition |
| Safety relief valve check | Monthly | SRV set point verification, mechanical condition, no evidence of weeping |
| Instrumentation check | Monthly | Pressure gauges reading within expected range, level indicators functional |
| Internal inspection | As per statutory schedule (typically every 4 years) | Internal corrosion, erosion, weld condition — requires specialist inspector and out-of-service state |

---

## 4. Routine Pump Inspection Procedure

The following procedure applies to all centrifugal process pumps in the KOC field equipment inventory. This procedure must be performed in the order listed. Steps may not be skipped or reordered. Skipping Step 1 through Step 4 before performing mechanical work may result in equipment energisation while personnel are in contact with moving parts, with potentially fatal consequences.

**Required tools:** Calibrated vibration analyser, IR thermometer, flow meter (portable ultrasonic), torque wrench, inspection mirror, flashlight, CMMS tablet or maintenance logbook.

**Prerequisite:** A valid Cold Work Permit must be in place before beginning Steps 6 through 9. Steps 1 through 5 may be performed under normal operational observation.

---

**Step 1 — Review maintenance history and P&ID.**
Before approaching the pump, retrieve the last three maintenance records from the CMMS. Review the Piping and Instrumentation Diagram (P&ID) for the pump circuit to understand all connected systems, isolation points, and instrumentation. Note any outstanding issues or open work orders.

**Step 2 — Don required PPE and conduct a site hazard assessment.**
Put on all mandatory PPE listed in Section 2.3. Walk the immediate work area and identify: overhead hazards, slip/trip hazards, hot surfaces, proximity to hydrocarbon lines, and any active nearby operations. Record findings on the pre-task hazard assessment form. Do not proceed if a hazard cannot be adequately controlled.

**Step 3 — Perform running visual and auditory inspection.**
With the pump in its normal operating state (do not shut it down for this step), observe the pump from a safe distance. Listen for unusual noise: grinding, rattling, or cavitation (a crackling sound). Look for: fluid leaks at seals or flanges, excessive vibration, abnormal temperatures indicated by discolouration or steam. Record baseline observations.

**Step 4 — Record operational data while pump is running.**
Using portable instruments, measure and record: suction pressure, discharge pressure, differential pressure, flow rate (if portable ultrasonic meter is available), motor current draw (from local panel or CMMS), bearing temperature at drive-end and non-drive-end bearings using the IR thermometer, and mechanical seal leakoff rate (drops per minute is acceptable for routine inspection). Compare all readings to the pump's baseline performance curve on file in the CMMS.

**Step 5 — Evaluate operational data before proceeding.**
Review the data collected in Step 4 against accepted operating ranges. If any reading falls outside the acceptable range, escalate per Section 6 (Escalation Criteria) before continuing. Do not proceed to mechanical inspection if the pump is exhibiting abnormal performance until the deviation has been documented and a Senior Engineer has assessed it.

**Step 6 — Initiate shutdown and apply LOTO.**
Notify the Control Room that the pump is being taken out of service for inspection. Follow the shutdown procedure on the pump's operating card. Once confirmed shut down, apply full LOTO per Section 2.2. Verify zero energy state before touching any mechanical components.

**Step 7 — Inspect mechanical seal, coupling, and external components.**
With LOTO applied and zero energy verified, inspect the mechanical seal face for wear, chipping, or heat damage. Check the seal flush piping for blockages. Inspect the coupling between motor and pump shaft for wear, cracking, or misalignment. Check bearing housing for oil leaks. Inspect all external bolts and flanges for corrosion, looseness, or damage. Tighten any loose bolts to the torque specification on the pump data sheet.

**Step 8 — Complete inspection documentation.**
Record all findings in the CMMS maintenance log for this pump. Note: component condition (Good / Monitor / Replace), any measurements taken, any anomalies found, work performed, parts replaced, and next recommended inspection date. If any components require replacement or further investigation, raise a corrective maintenance work order in the CMMS before leaving the site.

**Step 9 — Remove LOTO and return pump to service.**
Remove LOTO in strict accordance with Section 2.2. Notify the Control Room that LOTO is removed and the pump is ready to return to service. Re-start the pump following the standard start-up procedure. Monitor for the first 10 minutes of operation: confirm pressures and flow are within expected range, confirm no new leaks, confirm bearing temperatures are within normal range. Sign and close the PTW.

---

## 5. Logging a Maintenance Event

Every maintenance activity — whether routine inspection, corrective repair, or emergency response — must be logged in the CMMS. Incomplete logging is a procedural violation.

**Required fields for a maintenance log entry:**

1. Work Order Number (auto-generated by CMMS on creation of the work order)
2. Equipment Tag Number (unique identifier on the equipment nameplate)
3. Equipment Description and Location (e.g., "Centrifugal pump, crude transfer service, Well Pad 14A")
4. Date and time work started, date and time work completed
5. Name and employee number of all personnel who performed work
6. PTW number (mandatory for all non-routine work)
7. Description of work performed (be specific — "replaced mechanical seal" is acceptable; "did maintenance" is not)
8. Condition found on arrival (Good / Degraded / Failed)
9. Parts replaced (part number, description, quantity)
10. Condition on completion (Good / Requires follow-up)
11. Any anomalies observed that were not the primary work scope
12. Next preventive maintenance due date

Log entries must be submitted within 24 hours of work completion. Entries submitted after 48 hours require a written explanation. Entries older than 72 hours require supervisor approval.

---

## 6. Escalation Criteria — When to Stop Work and Call a Supervisor

A field engineer must stop work immediately and contact the Shift Supervisor if any of the following conditions are encountered:

1. **Any reading outside the safe operating envelope** — pressure, temperature, flow, or vibration readings that cannot be explained by normal variation.
2. **Unexpected release of any fluid or gas** — including small leaks that were not present at the start of the work.
3. **Visible fire, smoke, or sparks** — stop all work, follow fire response procedure in Safety Protocols document (KOC-OPS-SAFETY-001), and activate the nearest manual call point.
4. **H2S alarm activation** — any H2S alarm, regardless of level, requires work stoppage. Follow H2S procedures in KOC-OPS-SAFETY-001.
5. **Structural damage discovered** — cracks in pressure-containing equipment, vessel walls, pipe walls, or support structures.
6. **Equipment in a condition that does not match its maintenance history** — signs of undocumented repair, missing components, or evidence of an unreported incident.
7. **Uncertainty about any step in this procedure** — if a step is unclear or the situation differs from what this procedure describes, do not improvise. Stop, secure the work site, and call a supervisor.
8. **Personal injury** — stop all work, administer first aid as trained, activate emergency response per KOC-OPS-SAFETY-001.
9. **PTW conditions change** — if site conditions change after the permit was issued (e.g., nearby hot work begins, weather changes significantly, adjacent equipment is shut down unexpectedly), the PTW may no longer be valid. Suspend work and contact the Area Authority.

**The Shift Supervisor contact number must be on the field engineer's person at all times. In the absence of a mobile signal, use the site radio on Channel 3 (Operations).**

---

*Document maintained by KOC Field Operations — Maintenance Standards Group. For corrections or updates, raise a document change request through the KOC Document Management System.*
