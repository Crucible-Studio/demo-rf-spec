# Crucible Amendments

All amendments derive from Article I (Signal First) and/or Article II (Human in the Loop)
in CONSTITUTION.md. The governing Articles are unconditional and cannot be amended.

---

## Project-Specific Amendments

### Amendment 1 — Domain Primitives
*Traces to: Article I (Signal First)*
*Status: RATIFIED 2026-06-18*
*Project: Remote Farm Equipment Health Telemetry Node*

Every threshold, sensitivity setting, and algorithm parameter in this
project must cite one of these primitives. A constant that cannot be
cited is an Article I violation.

  P1 — RSSI (dBm)
       The received signal power of the last packet, read directly from
       the LoRa radio register — no arithmetic required. Degrades with
       free-space path loss and rain attenuation over the 8 km link.

  P2 — SNR (dB)
       The signal-to-noise ratio of the last received packet, read
       directly from the LoRa radio register. Determines whether the
       demodulator can recover the health hash at the base station.

Physical justification:
At 8 km in heavy rain (~5 days/week), two independent effects combine
to threaten link reliability: rain attenuation reduces RSSI toward the
sensitivity floor, and ambient noise raises the noise floor, compressing
SNR. Both must stay above their demodulation-floor thresholds for the
health hash packet to be decoded. RSSI and SNR are each read as a single
register value from the radio — they are first-order and require no
computed intermediaries. Together they constitute the complete physical
evidence base for every firmware threshold and filter parameter in this
project.

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
| 1 | Domain Primitives | RATIFIED 2026-06-18 | Article I |
| 2 | Stage Gate Order | PROPOSED | Article I + II |
| 3 | Toolchain Alignment | PROPOSED | Article II |
| 4 | Three-Strike Escalation Rule | PROPOSED | Article II |
