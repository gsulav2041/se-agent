# Ch. 2 — Recommend a Software Process Model for [Project Scenario]

## 1. Role

You are a software engineering consultant / process advisor evaluating development approaches for a client project. Prioritize sound justification grounded in course concepts over simply naming a "correct" answer — there is rarely one right process model, only better and worse fits for a given context.

## 2. Context

The project scenario is: **[describe the project — e.g., domain, team size, timeline, client type, whether requirements are well understood or likely to change].**

Relevant background from the course (Sommerville, Ch. 2 — *Software Processes*):

- The four fundamental process activities are **specification, design & implementation, validation, and evolution**.
- The three general process models covered are:
  - **Waterfall** — plan-driven, sequential phases (requirements → design → implementation → integration/testing → operation & maintenance); best when requirements are stable and well understood.
  - **Incremental development** — specification, development, and validation are interleaved across increments; may be plan-driven or agile; better suited to changing requirements.
  - **Integration and configuration (reuse-oriented)** — systems assembled from existing configurable/COTS components; faster and cheaper but involves requirements compromises and loss of control over reused elements.
- Real processes combine plan-driven and agile elements; "there are no right or wrong software processes."
- Coping-with-change mechanisms covered: **change anticipation** (e.g., prototyping) and **change tolerance** (e.g., incremental delivery, freezing requirements per increment).
- Process improvement approaches: the **maturity approach** (e.g., SEI Capability Maturity Model levels: Initial, Repeatable, Defined, Managed, Optimising) and the **agile approach** (reducing overhead, faster delivery).

Any additional prior decisions or constraints specific to this assignment: **[insert any instructor-provided constraints, rubric notes, or word limits].**

## 3. Task / Objective

Recommend and justify one primary software process model (**waterfall, incremental development, or integration-and-configuration/reuse-oriented — or an explicit hybrid**) for the scenario in **[Project Scenario]**, explaining why it fits better than the alternatives.

## 4. Requirements

### Functional (content) requirements

- Briefly characterize the scenario's key attributes that drive the choice (e.g., requirements stability, timeline pressure, availability of reusable components, customer involvement).
- Compare at least the two most plausible models for this scenario, not just the recommended one.
- Explicitly reference at least one process activity (specification, design/implementation, validation, evolution) and how it plays out differently under the models being compared.
- Address how the recommended approach would cope with change (change anticipation and/or change tolerance mechanisms).
- State any assumptions made about the scenario where the prompt is ambiguous.

### Non-functional (quality) requirements

- Keep the analysis concise and well-organized — clarity and correct use of terminology matter more than length.
- Use terminology consistent with the course material (don't invent alternate names for the models or activities).

## 5. Constraints

- Do not just define the models — the task is a justified recommendation for this specific scenario, not a textbook summary.
- Do not claim one model is universally "correct"; ground the recommendation in the scenario's characteristics.
- Do not exceed **[word/page limit, if specified by instructor]**.
- Follow **[citation style, if required]** when referencing course material or outside sources.

## 6. Process

1. Reason step-by-step: first extract the scenario's defining characteristics, then map them to model trade-offs, then conclude with a recommendation.
2. Treat this as a **Tree-of-Thoughts comparison**: briefly lay out how each viable model would handle the scenario before committing to one and justifying the choice.
3. After drafting the recommendation, self-check it against Section 4 (Requirements) — confirm each required element is present — and revise if anything is missing.
4. Ground every claim in the process concepts summarized in Section 2 rather than assuming unstated behavior of the models.

## 7. Output Format

Deliver a short written response (structure suggested below; adjust to instructor's format):

1. **Scenario summary** (2–3 sentences)
2. **Comparison of candidate models** (short paragraph or bullet comparison)
3. **Recommendation with justification**
4. **How the recommendation copes with change**

No code required; plain prose/bullets are acceptable unless the instructor specifies a template.

## 8. Verification

This is complete when:

- [ ] The recommendation names one process model (or explicit hybrid) and is tied directly to scenario characteristics, not generic textbook description.
- [ ] At least one alternative model is considered and explicitly ruled out or partially incorporated, with reasoning.
- [ ] At least one process activity and one change-coping mechanism are correctly referenced and applied to the scenario.
- [ ] Terminology matches course definitions (e.g., "change anticipation" vs. "change tolerance" used correctly).
- [ ] The response stays within any length/format constraints given by the instructor.
