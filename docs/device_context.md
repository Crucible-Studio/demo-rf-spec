# Device Context

This file is the primary evidence document for all agents operating under the
Crucible Constitutional Governance system.

**Agents: read this file before any hearing argument or advisory session.**

---

## Device Purpose

A LoRaWAN endpoint deployed at a remote farm site transmits health telemetry to a base station gateway. Farm operators depend on this link for continuous visibility into farm health; if the link fails, critical health events go undetected until someone physically visits the site. The hardest operating scenario is a wet summer — rain 5 days per week — which increases RF path loss and depresses received signal strength at the gateway. The device is considered working when its packet (device hash) is successfully received at a gateway 8 km away from the deployed unit.

**Project target:** Sustained LoRaWAN uplink in wet summer conditions with ~5 rain days per week at 8 km range.

**Pass/fail threshold:** Device hash packet received at gateway ≥ 8 km from the remote unit.

**Failure mode:** Packet loss at the gateway — farm health telemetry does not arrive and operators lose remote visibility into site conditions.

---

## Signal Inventory

> [To be filled by /spec collect]

---

## Bill of Materials (BOM)

> [To be filled after toolchain init]

---

## Test Results

> [To be filled after Stage 0]

---

## Open Anomalies

> [None yet]
