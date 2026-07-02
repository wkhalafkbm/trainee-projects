# Restricted Operational Parameters — Pipeline Segments P-101, P-102, P-103
**Document ID:** KOC-OPS-PARAMS-014
**Clearance Level: RESTRICTED** — Authorised for Senior Engineers (Grade SE-3 and above) and Shift Supervisors only. Distribution to General-clearance personnel is prohibited without written authorisation from the Field Operations Manager.
**Revision:** 2.7
**Last Updated:** April 2026
**Issuing Authority:** Kuwait Oil Company — Field Operations Division / Pipeline Integrity Group

---

> **ACCESS CONTROL NOTICE**
> This document contains operational parameters that, if misapplied, could result in equipment failure, hydrocarbon release, or personnel fatality. It is not a training document. Personnel unfamiliar with pipeline operations should not interpret or act on these parameters independently. If you have accessed this document without a Restricted clearance, notify your supervisor immediately and do not continue reading.

---

## 1. Purpose and Scope

This document defines the operational parameters for three pipeline segments in the Northern Gathering Area (NGA): P-101, P-102, and P-103. It covers safe operating envelopes for pressure and flow, temperature-based automatic shutdown (ASD) triggers, manual override procedures, and current operational status. This information is used by Senior Engineers and Control Room Supervisors to manage pipeline operations, investigate deviations, and authorise interventions.

This document must be reviewed and updated within 72 hours of any change to the operational parameters of these segments. Outdated parameter documents must not be used for operations decisions.

---

## 2. Pipeline Segment Descriptions

### P-101 — Northern Crude Transfer Main

**Service:** Crude oil transfer from NGA Well Cluster 4 to NGA Gathering Station 2
**Nominal Diameter:** 16 inches
**Design Pressure:** 120 bar(g)
**Design Temperature:** -10°C to 80°C
**Material:** Carbon steel, internally coated
**Commissioning Date:** September 2009
**Last Integrity Survey:** November 2025
**Cathodic Protection System:** Impressed current, active

### P-102 — Associated Gas Compression Feed Line

**Service:** Associated gas from NGA Separator Train B to Compression Station 7
**Nominal Diameter:** 10 inches
**Design Pressure:** 85 bar(g)
**Design Temperature:** -10°C to 65°C
**Material:** Carbon steel, externally coated
**Commissioning Date:** March 2014
**Last Integrity Survey:** August 2025
**Cathodic Protection System:** Sacrificial anode, last inspected June 2025

### P-103 — Produced Water Injection Line

**Service:** Treated produced water from NGA Water Treatment Unit to injection wells IW-04, IW-05, IW-06
**Nominal Diameter:** 8 inches
**Design Pressure:** 200 bar(g)
**Design Temperature:** 5°C to 70°C
**Material:** Duplex stainless steel
**Commissioning Date:** July 2018
**Last Integrity Survey:** February 2026
**Cathodic Protection System:** N/A (stainless steel)

---

## 3. Pressure Operating Ranges

The following operating ranges are the approved limits for normal, continuous operation. These are more conservative than the design limits and incorporate a safety factor based on pipeline age, condition data from the most recent integrity survey, and risk assessment. Do not confuse design pressure with operating pressure — operating beyond the maximum operating pressure is a procedural violation even if the design pressure has not been reached.

| Segment | Minimum Operating Pressure | Normal Operating Range | Maximum Operating Pressure | High-High Alarm (ASD Trigger) |
|---|---|---|---|---|
| **P-101** | 12 bar(g) | 45 – 72 bar(g) | 78 bar(g) | 82 bar(g) |
| **P-102** | 8 bar(g) | 28 – 54 bar(g) | 60 bar(g) | 64 bar(g) |
| **P-103** | 30 bar(g) | 110 – 155 bar(g) | 168 bar(g) | 175 bar(g) |

**Low Pressure Alarm:** If pressure falls below the minimum operating pressure, this may indicate a leak, line break, or upstream supply issue. A low pressure alarm does not trigger automatic shutdown but must be investigated within 15 minutes of alarm activation. If no cause is identified within 30 minutes, initiate controlled shutdown and notify the Field Operations Manager.

**Note on P-103:** The elevated design pressure of P-103 reflects the requirements of deep injection operations. P-103 operates at pressures significantly higher than P-101 and P-102. Valve operations and isolation procedures on P-103 must be performed with particular care due to the stored energy in the pressurised line. Rate of pressure change must not exceed 10 bar per minute during start-up or shutdown.

---

## 4. Flow Rate Operating Limits

Flow rates below are in standard cubic metres per hour (Sm³/h) for gas service (P-102) and cubic metres per hour (m³/h) for liquid service (P-101, P-103).

| Segment | Minimum Stable Flow Rate | Normal Operating Range | Maximum Allowable Flow Rate |
|---|---|---|---|
| **P-101** | 120 m³/h | 350 – 680 m³/h | 750 m³/h |
| **P-102** | 5,000 Sm³/h | 18,000 – 38,000 Sm³/h | 42,000 Sm³/h |
| **P-103** | 80 m³/h | 180 – 320 m³/h | 380 m³/h |

**Minimum Flow Considerations:**
- P-101: Operating below 120 m³/h for more than 10 minutes risks wax deposition and potential plugging. Notify the Pipeline Integrity Engineer if sustained low-flow operation is anticipated.
- P-102: Low flow below 5,000 Sm³/h may cause liquid accumulation in the line. Ensure liquid knockout facilities at Compression Station 7 are operational before reducing flow.
- P-103: Flow below 80 m³/h risks scale deposition at injection wellheads. Consult the Reservoir Engineer before operating below minimum flow.

**Maximum Flow Considerations:** Exceeding maximum allowable flow rate increases erosion rate and pressure drop. Any operation above the maximum allowable flow rate requires a written deviation approval from the Pipeline Integrity Group, valid for no more than 72 hours.

---

## 5. Temperature Thresholds and Automatic Shutdown Triggers

All three pipeline segments are equipped with temperature monitoring at inlet, midpoint, and outlet. Temperature deviations outside the following thresholds trigger automatic shutdown (ASD) of the associated feed pumps or compressors. ASD does not close isolation valves on P-101 or P-102 — manual valve isolation is required after an ASD event.

On P-103, ASD activates both the injection pump shutdown and automatic closure of the wellhead isolation valves (WIV) at IW-04, IW-05, and IW-06.

| Segment | Low Temp Alarm | Low Temp ASD | High Temp Alarm | High Temp ASD |
|---|---|---|---|---|
| **P-101** | 10°C | 5°C | 68°C | 74°C |
| **P-102** | 2°C | -3°C | 58°C | 62°C |
| **P-103** | 8°C | 3°C | 62°C | 67°C |

**ASD Response Procedure:**
1. The Control Room receives the ASD alarm and records the exact time, pipeline segment, and triggering parameter.
2. The Shift Supervisor is notified immediately.
3. Do not attempt to restart the pipeline without identifying and resolving the cause of the ASD.
4. A Senior Engineer must review the SCADA historian data for the 30 minutes prior to the ASD event before any restart is authorised.
5. Restart requires a written ASD clearance signed by the Shift Supervisor and a Senior Engineer.
6. If the cause of the ASD cannot be determined within two hours, the Pipeline Integrity Group must be consulted before restart.

---

## 6. Manual Override Procedures

> **WARNING — DUAL AUTHORISATION REQUIRED**
>
> Manual override of any automatic shutdown or control system on P-101, P-102, or P-103 is a high-risk activity. Overrides bypass protective systems that exist to prevent equipment damage, hydrocarbon release, and personnel injury. Under no circumstances may a single individual authorise or execute a manual override. Dual authorisation — from both the Shift Supervisor and a Senior Engineer of Grade SE-3 or above — is mandatory for every override action, without exception.
>
> Overrides performed without dual authorisation constitute a serious procedural violation and will be subject to formal investigation. In the event of an incident during an unauthorised override, individual liability may apply.

### 6.1 Conditions Under Which Override May Be Considered

Manual overrides are only justified in the following circumstances:

1. The ASD has been triggered by a confirmed instrumentation fault (sensor failure, transmitter drift), not by a genuine process condition. Instrument fault must be confirmed by the Instrument Technician in writing before the override is applied.
2. A planned operational manoeuvre requires temporary inhibition of a protection, and a formal written hazard review (Management of Change, MoC) has been completed and approved by the Operations Manager in advance.
3. A controlled shutdown is in progress and the override is required to sequence the shutdown safely — this must be pre-approved in the operating procedure for that shutdown.

### 6.2 Manual Override Procedure

1. The Senior Engineer identifies the specific protection to be overridden and documents the technical justification.
2. The Senior Engineer and Shift Supervisor complete the Override Authorisation Form (KOC-F-OVR-003). Both must sign. The form requires: the override type, the equipment tag, the justification, the expected duration, the compensating measures in place during the override period (e.g., increased manual monitoring frequency), and the criteria for restoring the protection.
3. The Control Room Operator applies the override in the DCS/SCADA system, records the override tag number, and sets a timer for the maximum authorised override duration.
4. During the override period, the Control Room Operator performs a manual scan of the overridden parameter every 15 minutes and logs each check.
5. The override is removed as soon as the condition justifying it no longer exists — and in any case before the authorised duration expires.
6. Override removal requires confirmation from both the Shift Supervisor and the Senior Engineer who authorised it.
7. The completed Override Authorisation Form is retained in the pipeline's technical file for a minimum of five years.

### 6.3 Emergency Override (Unplanned)

If a genuine emergency requires an immediate override without time to complete the full authorisation process:
1. The Shift Supervisor may authorise the override verbally and direct the Control Room Operator to apply it.
2. The verbal authorisation must be recorded in the Control Room log with a timestamp.
3. The Override Authorisation Form must be completed and signed within one hour of the override being applied.
4. The Field Operations Manager must be notified within 30 minutes of any emergency override.

---

## 7. Current Operational Status

*Status as of document revision date. Real-time status is available in the SCADA system — always refer to SCADA for current conditions. This table is for reference and planning purposes only.*

| Segment | Status | Current Operating Pressure | Current Flow Rate | Active Alarms | Notes |
|---|---|---|---|---|---|
| **P-101** | Normal Operation | 58 bar(g) | 490 m³/h | None | Pig receiver at GS-2 scheduled for Q3 2026. Coating survey pending scheduling. |
| **P-102** | Derated Operation | 46 bar(g) | 24,500 Sm³/h | Low Flow Advisory | Operating at reduced capacity pending compressor C-7B maintenance. Maximum operating pressure temporarily reduced to 58 bar(g) per MoC-2026-041. Do not operate above 58 bar(g) without Field Operations Manager approval. |
| **P-103** | Normal Operation | 138 bar(g) | 245 m³/h | None | IW-05 injection reduced 15% following well monitoring review. Reservoir Engineer consulted. No integrity concerns. |

**P-102 Derated Operation — Additional Note:** MoC-2026-041 is in effect until compressor C-7B is returned to service (target date: 15 July 2026). During this period, the High-High ASD trigger on P-102 is active at 62 bar(g) as normal. The temporary maximum operating pressure of 58 bar(g) is a procedural limit — it does not modify the ASD setpoint. Personnel operating P-102 during this period must be briefed on MoC-2026-041 before commencing operations. The MoC document is available in the document management system under project code NGA-2026-C7B.

---

## 8. Document Control and Review

This document must be reviewed:
- Every six months as a scheduled review
- Within 72 hours of any change to the operational parameters of P-101, P-102, or P-103
- Following any ASD event on any of these segments
- Following any inspection or integrity survey that results in a parameter change recommendation

Suggested changes to operating parameters require approval from: Pipeline Integrity Group (technical approval), Field Operations Manager (operational approval), and HSE Division (risk review). Changes may not be implemented until all three approvals are obtained and a revised document is issued.

Enquiries: pipeline.integrity@koc.com.kw / Field Operations duty phone (24h): available from site office.

---

*This document is classified Restricted. Unauthorised distribution, copying, or disclosure to non-authorised personnel is a violation of KOC Information Security Policy and may result in disciplinary action.*
