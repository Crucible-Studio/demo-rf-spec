# Demo SOP — RF Spec Session
## Buyer Visit — 2026-06-20 (Friday)

**Duration: 6–8 minutes**
**Format: Buyer answers 3 questions live, ratifies Amendment 1**

---

## Before the buyer walks in

```bash
cd /Users/siyaoshao/demo-rf-spec
claude
```

Terminal is open and sitting at the Claude Code prompt. Nothing typed yet.

---

## Step 1 — Frame it (20 seconds)

> "This is a blank project. The governance system knows nothing about the device.
> I'm going to type one command. It will ask you three questions.
> Your answers are the spec."

Type:
```
/spec collect
```

Hand control to the buyer — or relay their verbal answers.

---

## The three questions (agent asks these in order)

**Q1:** *"What does this device do — and what happens to a real person or system when it gets the answer wrong?"*

The buyer should name the device, the output, and the failure consequence.
Good answers are specific: "a logistics team gets a false all-clear and the shipment is quarantined."
Vague answers ("it could cause problems") are fine — the agent won't push.

**Q2:** *"What is the hardest physical environment this device has to work in?"*

This grounds the primitives in physics. Listen for a material constraint:
metal enclosure, underground, high EMI, extreme temperature, dense multipath.
"Indoors" is too vague — the agent will accept it but the primitives will be weaker.

**Q3:** *"When you're standing next to a deployed unit in that environment, what single number tells you it's working correctly?"*

This is the key question. The buyer will name a number that IS the primitive:
RSSI, SNR, link margin, SINR, PER, field strength — whatever they reach for first
is the answer their domain knowledge already knows.

**Do not interrupt.** Let the agent ask, let the buyer answer.

---

## After Q3 — what happens next (no action needed)

The agent extracts primitives from the three answers and prints the proposed Amendment 1.

**What to expect for a LoRa/cellular RF device:**
```
PROPOSED AMENDMENT 1 — Domain Primitives
Project: [device name]

  P1 — Received Signal Strength (dBm)
       First-order: read directly from the receiver hardware per packet.
       No arithmetic required. Governs the minimum sensitivity threshold
       and the coverage-loss alert condition.

  P2 — Signal-to-Noise Ratio (dB)
       First-order: read from the demodulator status register per packet.
       Governs spreading factor selection and demodulation floor.
       The SF12 sensitivity floor (−7.5 dB SNR) is a physical property
       of LoRa modulation, not a tuned constant — it traces here.

Physical justification:
In a metal container at 30–40 dB attenuation below open-air, RSSI and SNR
are the only quantities readable without bench equipment. Link margin
(RSSI − sensitivity) is a useful derived metric but traces to P1 — it is
not independently measurable. The pass/fail threshold (e.g. ≥12 dB margin)
anchors to P1 via the sensitivity spec of the modem at the active SF.

Do you ratify Amendment 1? (yes / no / revise)
```

---

## The ratification moment

Point to the buyer and say nothing. Let them decide.

If they want to change something — let them. The revision loop is the demo:
it shows the system is a tool for their domain knowledge, not a fixed template.

Once they say **yes** (or you type it), the agent writes the file and prints:

```
══════════════════════════════════════════════════════════════
AMENDMENT 1 RATIFIED
Primitives: Received Signal Strength (dBm) · Signal-to-Noise Ratio (dB)
Written to docs/governance/amendments.md
Every agent in this project reads these before acting.
══════════════════════════════════════════════════════════════
```

---

## Show the file (30 seconds)

Open `docs/governance/amendments.md`.

> "This is the constitutional record — written from your three answers.
> A firmware constant that doesn't cite one of those two primitives
> is an Article I violation. The code reviewer flags it. The police agent
> records it. The attorney cites it in any hearing."

---

## Optional contrast (60 seconds)

```bash
grep -A 6 "Amendment 1" /Users/siyaoshao/crucible-field-antenna/docs/governance/amendments.md | head -10
```

> "Our antenna diagnostics vertical has P1=S11, P2=VSWR, P3=Input impedance.
> Same RF domain — different primitives, because those came from a VNA bench workflow.
> Your device never sees a VNA in the field. Three questions about your actual deployment
> produced different physics than our pre-loaded template. That's the point."

---

## Timing

| Step | Time |
|------|------|
| Frame + `/spec collect` | 30 sec |
| Q1 — buyer answers | 1 min |
| Q2 — buyer answers | 1 min |
| Q3 — buyer answers | 30 sec |
| Agent derives + prints Amendment 1 | 1–2 min |
| Buyer reviews, optional revision | 1 min |
| Ratification + banner | 15 sec |
| Show file | 30 sec |
| Contrast (optional) | 1 min |
| **Total** | **~7 min** |

---

## If the buyer freezes on Q3

Q3 sometimes catches people off guard. Prompts you can use:

- "If you had a meter in your hand, what would you measure?"
- "What does your field team check when a unit stops reporting?"
- "What number in the dashboard tells you 'that device has good coverage'?"

Any of these unlocks the answer. Do not give them the answer — the whole point
is that it comes from their domain knowledge.
