Collect the device specification through a three-question interview. Writes docs/device_context.md and drafts Amendment 1 for human ratification.

Usage: /spec collect

---

## collect

Ask exactly three questions, one at a time. Wait for the complete answer before
asking the next. Do not summarise between questions. Do not suggest answers.
Do not ask follow-ups unless the answer is genuinely too ambiguous to extract
a primitive from — in that case, ask one clarifying question only.

---

### Question 1

Ask verbatim:

> "What does this device do — and what happens to a real person or system
> when it gets the answer wrong?"

Wait for full answer. Then ask Question 2.

---

### Question 2

Ask verbatim:

> "What is the hardest physical environment this device has to work in?"

Wait for full answer. Then check: does the answer contain at least one concrete
number, frequency, measurement, or physical quantity (e.g. "5 days/week",
"−40°C", "30 dB attenuation", "8 km", "90% humidity")?

- **Yes** → proceed to Question 3.
- **No** → ask this follow-up verbatim, once only:

  > "Can you put a number on that — how often, how severe, or how far?
  > Anything concrete."

  Wait for the answer, then proceed to Question 3 regardless of whether
  a number was given.

---

### Question 3

Ask verbatim:

> "When you're standing next to a deployed unit in that environment,
> what single number tells you it's working correctly?"

Wait for full answer. Then proceed immediately — no more questions.

---

### After Question 3 — challenge derived metrics first

Before extracting primitives, evaluate the number the human named in answer 3:

- Is it **first-order** — readable directly from a sensor or instrument register
  with no arithmetic on other measured values? → it is a primitive candidate
- Is it **derived** — a ratio, difference, or computed score that depends on two
  or more other quantities? → it is not a primitive

**If the answer-3 number is derived**, say so explicitly before proceeding:

> "That's a derived metric — it traces to [underlying quantity A] and
> [underlying quantity B]. I'll use those as the primitives. [Derived metric]
> is the pass/fail outcome, but [A] and [B] are what the firmware actually
> measures."

Then continue. Do not ask another question — identify the underlying primitives
from the domain context and proceed.

Examples of derived metrics that must be resolved this way:
- Link margin (RSSI − sensitivity floor) → traces to RSSI
- Hash integrity / packet error rate → traces to RSSI + SNR
- SNR margin → traces to SNR
- A computed score or index → traces to its input measurements

---

### Extract primitives

Extract 2–3 domain primitives from all three answers. Rules:

- A primitive is a **first-order physically measurable quantity** — something
  the device ultimately depends on that can be read from a sensor or instrument
  directly, with no arithmetic on other measured values
- If the human named a derived metric in answer 3, use the underlying primitives,
  not the derived metric itself
- 2 primitives is usually correct; 3 if the device genuinely has two independent
  physical domains; never more than 3 for a first spec

---

### Write Device Purpose

Write to `docs/device_context.md` ## Device Purpose using the human's exact words:

```markdown
## Device Purpose

[One paragraph from answers 1–3: what the device does, who depends on it,
the hardest scenario, and the failure mode with its real-world consequence.]

**Project target:** [hardest scenario from answer 2, one sentence]

**Pass/fail threshold:** [the primitive measurements from the extracted P1/P2,
with the value or limit. If the human named a derived metric, write:
"[Derived metric] ≥ [limit] — traces to P1 ([primitive name]) and P2 ([primitive name])"]

**Failure mode:** [from answer 1 — what goes wrong and for whom]
```

---

### Draft Amendment 1

Print the proposed amendment — do NOT write to amendments.md yet:

```
═══════════════════════════════════════════════════════════════
PROPOSED AMENDMENT 1 — Domain Primitives
Project: [device name]
Traces to: Article I (Signal First)

Every threshold, sensitivity setting, and algorithm parameter in this
project must cite one of these primitives. A constant that cannot be
cited is an Article I violation.

  P1 — [name] ([unit])
       [one sentence: what it measures physically and why it is first-order]

  P2 — [name] ([unit])
       [one sentence]

  [P3 — if and only if the device has a second independent physical domain]

Physical justification:
[One paragraph: why these primitives ground the pass/fail threshold from
answer 3, and why the hardest scenario from answer 2 requires measuring them.]

Do you ratify Amendment 1? (yes / no / revise)
═══════════════════════════════════════════════════════════════
```

---

### On ratification

**yes:** Write the ratified amendment to `docs/governance/amendments.md` under
`## Project-Specific Amendments`. Mark the Amendment Index row RATIFIED with
today's date. Print exactly:

```
══════════════════════════════════════════════════════════════
AMENDMENT 1 RATIFIED
Primitives: [P1 name] · [P2 name] [· P3 if applicable]
Written to docs/governance/amendments.md
Every agent in this project reads these before acting.

Next steps:
  1. Run agent-updater — propagates these primitives to all 17 agents
  2. /toolchain init  — registers your hardware and locks the toolchain
══════════════════════════════════════════════════════════════
```

Print nothing else after this block.

**revise:** Ask what to change. Apply the change and print the revised amendment.
Ask for ratification again.

**no:** Acknowledge and note that Amendment 1 must be ratified before /session 0 can run.

---

Now parse "$ARGUMENTS". If subcommand is `collect` or empty, run the three-question
interview above. For any other subcommand, print usage and stop.
