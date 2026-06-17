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

Wait for full answer. Then ask Question 3.

---

### Question 3

Ask verbatim:

> "When you're standing next to a deployed unit in that environment,
> what single number tells you it's working correctly?"

Wait for full answer. Then proceed immediately — no more questions.

---

### After Question 3 — extract primitives

Extract 2–3 domain primitives from all three answers. Rules:

- A primitive is a **first-order physically measurable quantity** — something
  the device ultimately depends on that can be read from a sensor or instrument
  directly, with no arithmetic on other measured values
- Every number the human named in answer 3 is a strong candidate
- A quantity that is the difference or ratio of two other quantities is **derived**,
  not primitive — note it traces to whichever primitive it is computed from
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

**Pass/fail threshold:** [the number from answer 3 with its unit and limit]

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
today's date. Print:

```
══════════════════════════════════════════════════════════════
AMENDMENT 1 RATIFIED
Primitives: [P1 name] · [P2 name] [· P3 if applicable]
Written to docs/governance/amendments.md
Every agent in this project reads these before acting.
══════════════════════════════════════════════════════════════
```

**revise:** Ask what to change. Apply the change and print the revised amendment.
Ask for ratification again.

**no:** Acknowledge and note that Amendment 1 must be ratified before /session 0 can run.

---

Now parse "$ARGUMENTS". If subcommand is `collect` or empty, run the three-question
interview above. For any other subcommand, print usage and stop.
