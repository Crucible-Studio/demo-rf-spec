# LoRaWAN Farm Sensor — Crucible RF Spec

Constitutional governance project for a LoRaWAN endpoint deployed at a remote farm site.
Amendment 1 ratified: **P1 = RSSI (dBm) · P2 = SNR (dB)**.

---

## The Device

A LoRaWAN endpoint transmits farm health telemetry to a base station gateway. Farm operators
depend on this link for continuous remote visibility; a silent link means critical events go
undetected until a physical site visit.

**Project target:** Sustained LoRaWAN uplink in wet summer conditions — ~5 rain days per week —
at 8 km range.

**Pass/fail threshold:** Device hash packet received at gateway ≥ 8 km from the deployed unit.

**Failure mode:** Packet loss. Farm health telemetry does not arrive. The operator has no remote
visibility into site conditions.

See [`docs/device_context.md`](docs/device_context.md) for the full evidence record.

---

## Why RSSI and SNR

The 8 km pass/fail threshold is a link budget problem. The transmitted packet survives only when
the gateway sees RSSI above its sensitivity floor **and** SNR above the LoRa demodulation floor
for the active Spreading Factor.

Wet conditions (5 rain days per week) add Mie scattering attenuation at 868/915 MHz, depressing
both quantities simultaneously. Every threshold, retry count, Spreading Factor selection, and TX
power parameter in this firmware ultimately traces to keeping RSSI and SNR within recoverable
bounds at 8 km range in rain.

**Link margin** (RSSI − sensitivity) is a useful derived metric but it traces to P1 — it is not
independently measurable and is not a primitive.

Amendment 1 is ratified. See [`docs/governance/amendments.md`](docs/governance/amendments.md).

---

## Constitutional Framework

This project runs under Crucible Constitutional Governance:

### Article I — Signal First

Every threshold, sensitivity setting, and algorithm parameter must cite a domain primitive.
A constant that cannot be cited is an Article I violation. For this device: all constants
trace to P1 (RSSI) or P2 (SNR).

### Article II — Human in the Loop

Agents execute. Humans decide. Any action whose consequence cannot be fully reversed by a
single `git revert` requires explicit human approval before execution.

---

## What Is Already Ratified

| Amendment | Title | Primitives |
|-----------|-------|------------|
| 1 | Domain Primitives | P1 = RSSI (dBm) · P2 = SNR (dB) |

Amendments 2 (Stage Gate Order), 3 (Toolchain Alignment), and 4 (Three-Strike Escalation)
are PROPOSED — ratify before `/session 0`.

---

## Governance Record

| File | Purpose |
|------|---------|
| [`CONSTITUTION.md`](CONSTITUTION.md) | Full governance model — Articles, Branches, processes |
| [`docs/governance/amendments.md`](docs/governance/amendments.md) | All ratified amendments |
| [`docs/governance/case_law.md`](docs/governance/case_law.md) | Judicial hearing rulings |
| [`docs/device_context.md`](docs/device_context.md) | Device purpose, BOM, signal inventory, test results |
| [`CLAUDE.md`](CLAUDE.md) | Agent entry point — what every agent reads on session start |

---

## Starting a Session

```bash
# See current project state
/session status

# Run the next development stage
/session 0       # HIL toolchain lock
/session 1       # Simulation
/session 2       # Firmware integration
```

If you are new to Crucible, read [`ONBOARDING.md`](ONBOARDING.md) first (15 minutes).

---

## Starting a New RF Project from This Template

This repo can be forked to start a new RF device project:

```bash
# Interview collects device context and drafts Amendment 1
/spec collect
```

Three questions. Your answers define the primitives. Amendment 1 is ratified by you — the agent
derives, you decide. The same interview that produced P1=RSSI/P2=SNR for this device would
produce different primitives for a bench RF diagnostic tool (P1=S11, P2=VSWR) — because
deployment context, not intuition, determines what is measurable.

---

## The Name

A crucible is the vessel in which materials are subjected to extreme conditions to test and
refine their properties. You do not declare a material pure because it looks right. You measure it.
