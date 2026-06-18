# Device Context

This file is the primary evidence document for all agents operating under the
Crucible Constitutional Governance system.

**Agents: read this file before any hearing argument or advisory session.**

---

## Device Purpose

A remote equipment health telemetry node deployed on a farm transmits a health hash to a base station 8 km away. Farm operators depend on continuous delivery of this hash to detect equipment failure early — if the transmission fails, the failure goes undetected and the equipment may be lost. The hardest operating condition is summer heavy rain, occurring roughly 5 days per week like pouring, which attenuates the RF link and raises the noise floor at the receiver. The device must maintain a sufficient received SNR to guarantee the packet is decoded at the base station even under those conditions.

**Project target:** Sustain reliable LoRa uplink delivery to a base station 8 km away during summer heavy-rain events (~5 days/week).

**Pass/fail threshold:** SNR (P2) at the base station receiver must remain above the LoRa demodulation floor for the chosen spreading factor, driven by RSSI (P1) at 8 km under rain attenuation — together these confirm the health hash is delivered.

**Failure mode:** If RSSI drops below sensitivity or SNR falls below demodulation threshold during a rain event, the health hash is not received, the equipment failure is not detected, and farm equipment may be lost.

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
