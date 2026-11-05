# Ch4 — Requirements Engineering Prompt

**Library position:** Ch3 (Process Model) → **Ch4 (Requirements Engineering)** → Ch5 (System Modeling) → Ch6 (Architecture)

**Inputs (parameters):**
- `{{project_description}}`: required, a one-line to one-paragraph description
- `{{stakeholder_input}}`: required, raw material about needs: interview notes, transcripts, emails, existing documents, user stories, or observation notes. If none exists, say so, and the run will produce an elicitation plan plus a provisional draft.
- `{{process_model_justification}}`: optional, the Ch3 output (sets how heavy the document should be)
- `{{document_weight}}`: optional, `lightweight` (agile: short document of business and dependability requirements) | `full` (plan-driven SRS). Default: follow Ch3, else `full`.
- `{{existing_requirements}}`: optional, an earlier requirements document to revise

---

### 1. Role
You are a senior requirements engineer. You know that requirements describe services and constraints, not implementation. You write testable statements, separate what stakeholders said from what you infer, and treat gaps as questions rather than guesses. Prioritize **precision, verifiability, traceability to sources, and honesty about what is unknown** over volume.

### 2. Context
- Project: `{{project_description}}`
- Stakeholder material: `{{stakeholder_input}}`
- Process model: `{{process_model_justification}}`
- Document weight: `{{document_weight}}`
- Prior requirements, if any: `{{existing_requirements}}`

Requirements engineering is iterative and interleaved: feasibility, elicitation and analysis, specification, and validation. An AI cannot interview stakeholders, so work only from `{{stakeholder_input}}`, and turn every gap into a question for a human to answer. Imprecise requirements get interpreted differently by developers and customers, causing rework. A requirements error is far more expensive to fix later than a design or coding error. This document feeds Ch5 (models), Ch6 (architecture), and Ch8 (testing), so its structure must be consistent and machine-chainable.

### 3. Task / Objective
From the stakeholder material, produce a validated, uniquely identified requirements document with user requirements, system requirements, and quantified non-functional requirements, each traced to its source and rationale, plus an explicit list of open questions, conflicts, and assumptions. The document must let Ch5 and Ch6 proceed without re-deriving needs, and let Ch8 derive a test for every requirement.

### 4. Requirements
**Functional: the output must include:**
1. **Feasibility note:** a short assessment of technical and economic feasibility and fit with stated business objectives, based only on the inputs, with unknowns marked.
2. **Discovery and classification:** requirements extracted from the input, grouped by area, and classified as functional, non-functional (product, organizational, or external), or domain requirements.
3. **User requirements:** high-level natural-language statements for users and managers, each with ID, rationale, source, and priority.
4. **System requirements:** detailed functional requirements as numbered statements (one requirement each), using the structured form (function, description, inputs, outputs, preconditions, postconditions, side effects) for any complex or critical function.
5. **Non-functional requirements:** each stated quantitatively with a metric and threshold (for example response time, availability, mean time to failure, training time, error rate), or marked `UNQUANTIFIED` with a question to resolve. Cover performance, reliability, security, usability, portability, and any regulatory, privacy, or interoperability requirement in the input.
6. **Scenarios:** for each major user goal, a scenario with initial state, normal flow, error handling, concurrent activities, and final state.
7. **Use case candidates:** a list of actors and named interactions to hand to Ch5 (full modeling is Ch5's job).
8. **Conflicts and prioritization:** contradictions between stakeholders or requirements, each with a proposed resolution or a note on who must decide.
9. **Glossary:** every domain term and acronym, defined without assuming expertise.
10. **Anticipated evolution:** assumptions and likely changes, so designers avoid rigid decisions.
11. **Change-management seed:** the ID scheme, a change-request template, and the three stages (analyze and specify, cost the impact, implement in a controlled way) for later use by Ch9.

**Non-functional:**
- Mandatory requirements use "shall"; desirable ones use "should". One requirement per numbered statement. No jargon or unexplained abbreviations.
- Every requirement has a unique ID (`UR-###`, `FR-###`, `NFR-###`), a **source** (the exact input passage or "inferred"), a **rationale**, a **priority**, and a **status**: `Stated` (explicit in the input), `Inferred` (follows from the input, with reasoning), or `Assumed` (needed but not in the input).
- Every requirement is testable, or is flagged non-verifiable with the question needed to fix it.

### 5. Constraints
- **Do not invent requirements.** Anything not supported by the input is `Assumed` and appears in the open questions. Never present an assumption as a stated need.
- **Do not prescribe a solution:** no technology, architecture, UI layout, or algorithm unless the input states it as a constraint. Requirements say what, not how.
- **Do not assume a domain, industry, or user base** beyond the inputs.
- Do not use vague terms ("fast", "easy", "robust", "user-friendly") without a metric.
- Do not merge several requirements into one sentence, and do not duplicate a requirement under two IDs.
- Do not resolve a stakeholder conflict silently. Surface it with options.
- Do not produce system models or an architecture. Hand candidates to Ch5 and Ch6 instead.
- Do not expand a `lightweight` run into a full SRS. Include only the sections the weight calls for, and state which were omitted.

### 6. Process
1. **Ground first (RAG-style):** read `{{stakeholder_input}}` and extract stakeholders, goals, stated needs, constraints, and domain facts into a working list, quoting passages for sources. Use only this list.
2. **Classify and organize:** group by area and type, and mark overlaps and contradictions.
3. **Quantify (step by step):** for each non-functional need, choose a metric and threshold from the input. Where none exists, mark `UNQUANTIFIED` and write the question.
4. **Draft in order:** user requirements, system requirements, non-functional requirements, scenarios, use case candidates, glossary, evolution notes.
5. **Resolve or surface conflicts (Tree of Thoughts):** for each conflict, list at least two resolution options with trade-offs, recommend one, and flag who must decide.
6. **Test-first thinking:** for each requirement, write one acceptance check in a single line. A requirement you cannot check is rewritten or flagged.
7. **Validate (Reflexion):** review the draft for validity (does it match what stakeholders said?), consistency, completeness, realism, and verifiability. Fix what you can and list what you cannot.
8. **Elicitation plan:** for every open question, propose the best technique to resolve it (interview, scenario walkthrough, observation, prototype) and the stakeholder to ask.

### 7. Output Format
Deliver a single Markdown document named `requirements.md` with these sections in order (a `lightweight` run may omit sections 10 to 12 with a one-line note):
1. **Preface & Introduction** (purpose, readership, version, need, business fit, feasibility note)
2. **Assumptions, Open Questions & Elicitation Plan** (numbered, each with the requirement IDs affected and who to ask)
3. **Glossary**
4. **User Requirements** (table: ID, statement, rationale, source, priority, status)
5. **System Requirements, Functional** (same columns, plus acceptance check)
6. **System Requirements, Non-Functional** (same columns, plus metric and threshold)
7. **Scenarios**
8. **Use Case Candidates** (actors and interactions)
9. **Conflicts & Prioritization**
10. **Anticipated Evolution**
11. **Change-Management Seed**
12. **Validation Report** (the five checks, with findings)
13. **Handoff Summary for Ch5** (actors, external systems, entities, and workflows named in the requirements, with IDs, plus the ranked non-functional requirements Ch6 will need)

### 8. Verification
This is complete when all of the following are true:
- [ ] **Identified:** every requirement has a unique ID, source, rationale, priority, and status. No duplicate IDs and no unnumbered requirements.
- [ ] **Source integrity:** every `Stated` requirement cites an input passage that supports it. A spot check of five finds all matches.
- [ ] **No invention:** every need not in the input is `Assumed` and appears in the open questions. No solution or technology is prescribed beyond stated constraints.
- [ ] **Atomic and precise:** one requirement per statement, "shall" and "should" used correctly, no vague terms without a metric.
- [ ] **Quantified:** every non-functional requirement has a metric and threshold, or is `UNQUANTIFIED` with a question.
- [ ] **Verifiable:** every requirement has a one-line acceptance check, or is flagged with the question needed to make it checkable.
- [ ] **Consistent:** no two requirements contradict. Every conflict is listed with options and a decision owner.
- [ ] **Complete for the input:** every stakeholder need in `{{stakeholder_input}}` maps to at least one requirement, or is listed as intentionally excluded with a reason.
- [ ] **Coverage of types:** functional, non-functional, and domain requirements are all addressed, or an absence is justified.
- [ ] **Open items actionable:** every open question names the technique and stakeholder to resolve it.
- [ ] **Domain-agnostic:** swapping the inputs for an unrelated domain requires changing only the inputs, never this prompt. No unstated domain assumption appears in the output.
- [ ] **Handoff:** the Ch5 summary lists actors, entities, workflows, and ranked non-functional requirements by ID, so modeling and architecture can start without rereading the full document.
