# Crucible Amendments

All amendments derive from Article I (Signal First) and/or Article II (Human in the Loop)
in CONSTITUTION.md. The governing Articles are unconditional and cannot be amended.

---

## Project-Specific Amendments

### Amendment 1 — Domain Primitives
*Traces to: Article I (Signal First)*
*Status: RATIFIED — 2026-06-17*

Every threshold, sensitivity setting, and algorithm parameter in this
project must cite one of these primitives. A constant that cannot be
cited is an Article I violation.

  P1 — RSSI (dBm)
       The power of the received LoRa signal measured directly at the
       gateway radio chipset (SX127x/SX126x register read); no arithmetic
       on other measured values. Whether the 8 km link closes under rain
       traces entirely to RSSI exceeding the gateway's sensitivity floor.

  P2 — SNR (dB)
       Signal-to-Noise Ratio reported directly by the gateway LoRa
       chipset per received packet. LoRa has a defined demodulation
       floor per Spreading Factor (e.g., −20 dB at SF12); a packet is
       recoverable only when SNR exceeds that floor. Rain increases
       path loss, directly depressing SNR independent of RSSI.

Physical justification:
The 8 km pass/fail threshold is a link budget problem: the transmitted
packet survives only when the gateway sees RSSI above its sensitivity
floor AND SNR above the LoRa demodulation floor for the active Spreading
Factor. Wet conditions (5 rain days/week) add Mie scattering attenuation
at 868/915 MHz, compressing both quantities simultaneously. Any
threshold, retry count, Spreading Factor selection, or TX power
parameter in this firmware ultimately traces to keeping RSSI and SNR
within recoverable bounds at 8 km range in rain.

---

## Mandatory Framework Amendments

### Amendment 2 — Stage Gate Order
*Traces to: Article I + II*
*Status: PROPOSED — ratify before /session 0*

Development proceeds through exactly these stages in order, and no stage begins
until the previous stage's exit criteria are explicitly confirmed by the human.

---

### Amendment 3 — Toolchain Alignment
*Traces to: Article II*
*Status: PROPOSED — ratify before /session 0*

Every agent must operate within the toolchain recorded in `docs/toolchain_config.md`.
No agent may introduce a new toolchain without a Bill enacted through the Legislative Process.

---

### Amendment 4 — Three-Strike Escalation Rule
*Traces to: Article II*
*Status: PROPOSED — ratify before /session 0*

If a simulation, test, or iterative fix fails within three attempts, the agent must
stop and wait for human direction before any further action.

---

## Amendment Index

| # | Title | Status | Traces to |
|---|-------|--------|-----------|
| 1 | Domain Primitives | RATIFIED 2026-06-17 | Article I |
| 2 | Stage Gate Order | PROPOSED | Article I + II |
| 3 | Toolchain Alignment | PROPOSED | Article II |
| 4 | Three-Strike Escalation Rule | PROPOSED | Article II |
