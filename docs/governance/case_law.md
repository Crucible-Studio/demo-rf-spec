# Crucible Case Law — GaitSense

This file records all Judicial Hearing rulings. Entries are written by the prevailing
attorney immediately after the Justice's ruling, before any implementation begins.

Live entries accumulate full argument text. Frozen entries (after stage closeout via
`stage-compactor`) contain only the compact operational record.

---

## Active Precedents

---

### Case 1: The Stair Walker Case
**Date:** 2026-03-27
**Positions:** A — Maintain dual-confirmation gate; correct for all profiles that passed validation | B — Dual-confirmation gate embeds terrain-specific assumption not derived from any walking primitive; must be replaced
**Prevailing position:** B
**Justice's ruling:** The dual-confirmation gate is replaced by the push-off primary detector with retrospective ring-buffer heel-strike inference. Any future step detector primary trigger must be a signal feature that is biomechanically required on all terrains and derivable from at least one walking primitive.
**Physical/empirical basis:** Signal diagnostic: gyr_y zero-crossing at 53ms, acc_filt peak at 188ms on stairs — temporal gap of 135ms. The 40ms confirmation window was derived from flat-ground heel-strike kinematics where both events are co-incident. This assumption cannot be derived from P1, P2, or P3. Push-off plantar-flexion (gyr_y) traces directly to P2 (cadence) and is biomechanically required on every terrain without exception.
**Device outcome protected:** Step detection on all terrain profiles (flat, bad_wear, slope, stairs) without terrain classification or parameter re-tuning. 100/100 steps detected on stair profile after fix vs 0/100 before.
**Conditions:** Time-gated co-occurrence windows that assume simultaneous signal events are not permitted unless the simultaneity is derived from and bounded by a walking primitive.
**Enacted bill (if any):** Push-Off Primary Step Detector (Option C)
**Implementation branch:** constitution-style-management

---

### Case 2: The Terrain Gate Case
**Date:** 2026-03-27
**Positions:** A — acc_mag gate references a shared quantity; may be cross-layer coupling | B — acc_mag gate (|acc_mag − 9.81| < 2.94) derived from flat-ground physics; must be replaced with terrain-agnostic gate from walking primitive
**Prevailing position:** B
**Justice's ruling:** Gate replaced with |gyr_y| < 20 dps. Article I takes precedence. Any phase transition gate that references a computed quantity must justify its terrain-invariance; if it cannot, it must be replaced by a raw axis gate derivable from walking primitive mechanics.
**Physical/empirical basis:** Stair walker stuck permanently in LOADING phase. acc_mag at stair mid-stance ≈ 20 m/s² due to heel-strike impact. Gate: |20 − 9.81| = 10.2 >> 2.94 — never fires. Heel-strike arrest decays from 37–60 dps to near-zero in ~100ms on all terrains; early ankle rocker is 10–13 dps. The 20 dps bisection point is terrain-invariant (derived from gyr_y decay dynamics of foot-floor contact, governed by stance mechanics, not surface type).
**Device outcome protected:** Phase segmenter correctly transitions on all terrain profiles. VSQRT.F32 Renode workaround removed (acc_mag computation eliminated).
**Conditions:** Computed quantities used in phase transition gates require explicit terrain-invariance justification traceable to a walking primitive. Flat-ground-derived thresholds are not terrain-invariant by default.
**Enacted bill (if any):** Terrain-Agnostic Phase Gate
**Implementation branch:** constitution-style-management

---

### Case 3: The Algorithm Comparison Case
**Date:** 2026-03-28
**Positions:** A — Three algorithm options (threshold tuning, filter redesign, push-off primary) were evaluated; Option C selected after exhausting A and B — valid domain search under Amendment 8 | B — Option C adds firmware complexity; hardware alternative (shoe-dorsum sensor) not formally evaluated as required by Amendment 9
**Prevailing position:** A
**Justice's ruling:** Option C accepted. However, shoe-dorsum mounting option is not closed — documented as open hardware iteration item. An agent may not remove this item without a new hearing. BOM alternatives are never silently closed by algorithm success alone.
**Physical/empirical basis:** Options A and B: 0/100 steps on stair profile. Option C: 100/100 steps, SI = 0.41% on stairs. RAM overhead: 32 bytes for ring buffer (0.03% of 118KB SRAM). Shoe-dorsum mounting: requires different form factor, different strap BOM, different user calibration — cost exceeds 32 bytes of firmware complexity. Option C also resolves bad_wear SI underestimation in pathological mode.
**Device outcome protected:** Terrain-aware detection on all four profiles. Hardware alternative preserved as open option.
**Conditions:** When an algorithm fix is accepted, the hardware alternative that was considered but not selected must be explicitly documented as an open option. Hardware iteration optionality survives algorithm success.
**Enacted bill (if any):** Push-Off Primary Step Detector (Option C)
**Implementation branch:** constitution-style-management

---

## Frozen Precedents

*(Populated by stage-compactor at each stage gate.)*
