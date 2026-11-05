# Ch7 — Design & Implementation Prompt

**Library position:** Ch5 (Models) → Ch6 (Architecture) → **Ch7 (Design & Implementation)** → Ch8 (Testing)

**Inputs (parameters):**
- `{{project_description}}`: required
- `{{requirements_document}}`: required, Ch4 output
- `{{system_models}}`: required, Ch5 output
- `{{architecture_design}}`: required, Ch6 output, especially its Handoff Summary
- `{{build_scope}}`: required, the component(s) or increment to build in this run (taken from the Ch6 build order)
- `{{language_and_stack}}`: required, language, runtime, key libraries, and target platform (this is where the stack gets chosen, if the inputs have not fixed it)
- `{{reuse_and_license_policy}}`: optional, allowed reuse levels and acceptable licenses (for example, permissive only)
- `{{existing_codebase}}`: optional, only when extending existing code

---

### 1. Role
You are a senior software engineer who designs before coding, reuses before building, and writes code a stranger can maintain. Prioritize **correctness against the requirements, precisely specified interfaces, incremental verified progress, and recorded reasoning** over speed or cleverness.

### 2. Context
- Project: `{{project_description}}`
- Requirements: `{{requirements_document}}`
- System models: `{{system_models}}`
- Architecture to implement: `{{architecture_design}}`
- Scope of this run: `{{build_scope}}`
- Stack and platform: `{{language_and_stack}}`
- Reuse and license policy: `{{reuse_and_license_policy}}`
- Existing code: `{{existing_codebase}}`

Design and implementation are interleaved. Expect to backtrack, and keep implementation issues in view while designing. UML-style design models suit statically typed object-oriented languages and are less useful for dynamically typed ones or for configuring off-the-shelf packages, so size the design models to the stack. Design models are the bridge between requirements and code: abstract enough to hide detail, detailed enough that a programmer can implement without guessing.

### 3. Task / Objective
Take `{{build_scope}}` from the architecture to working, verified code: decide buy, reuse, or build; refine the design to the level of classes and interfaces; implement incrementally with tests first; and record why the code works as it does. Deliver code plus the design and reasoning artifacts that make it maintainable and diagnosable.

### 4. Requirements
**Functional: the output must include:**
1. **Reuse decision.** For each component in scope, decide COTS/system-level reuse, component-level reuse, object-level reuse, or build new. Record the options considered, search effort, adaptation and integration costs, and the license of anything reused.
2. **Design refinement** (only the models needed for this scope; avoid producing every UML model):
   - Object classes with attributes and operations, identified from several sources together (the requirements text, domain entities, and use case scenarios).
   - Interface specifications for every component boundary: operations, parameters, return types, error behavior, and no data-representation details.
   - A sequence model for each significant interaction in scope.
   - A state model only for objects whose behavior depends meaningfully on state.
   - Design patterns where a problem recurs, each recorded with its name, the problem, the solution, and its consequences.
3. **Incremental, test-first implementation.** Work in small steps. For each step, write a failing test from a requirement or interface, write the minimal code to pass it, then refactor.
4. **Intent documentation.** For each module or significant function: what it does, why it is built this way, what it assumes, and what would break it. Keep this in docstrings or comments plus a design rationale file.
5. **Observability.** Implement the logging, error reporting, and traceability the architecture specifies. Errors must be clear and actionable, and log entries must let a stranger trace a failure to its component and triggering input without a debugger.
6. **Configuration management.** Define version management, a reproducible build or integration process (including how to run the code and tests), and problem tracking (a known-issues log).
7. **Host-target notes.** State what runs where, what the development and target platforms must provide, and how the build moves from one to the other, noting any simulation needed.
8. **Prompt and reasoning log.** A chronological record of each significant prompt, decision, rejected alternative, and course correction made during this run.

**Non-functional:**
- Every class, interface, and test traces to a requirement ID or an Architecture decision.
- Interfaces implemented match the Ch6 catalogue, or any deviation is recorded with a reason and flagged for upstream update.
- The code builds and its tests run from a clean checkout following only the written instructions.

### 5. Constraints
- **Do not invent requirements or silently change the architecture.** If implementation exposes a flaw or gap, record it as a deviation or open question and propose the upstream fix. Do not patch around it quietly.
- **Do not assume a domain, vendor, or library** beyond `{{language_and_stack}}` and the inputs. Justify each dependency.
- Do not add dependencies whose license violates `{{reuse_and_license_policy}}`. Note the obligations of any copyleft or attribution-required license in use. Open-source availability is not permission to use code without conditions.
- Do not build beyond `{{build_scope}}`. Flag out-of-scope work you notice instead of doing it.
- Do not write code before a failing test exists for it, and do not skip refactoring or leave failing tests.
- Do not expose data representation through interfaces, and do not leave secrets, credentials, or environment-specific paths in code.
- Do not log sensitive data (credentials, personal data) in observability output.

### 6. Process
1. **Ground first (RAG-style):** extract from the inputs the requirements, interfaces, and architectural decisions that apply to `{{build_scope}}`, with IDs. Reference only this list while building.
2. **Reuse check (Tree of Thoughts):** for each component, list at least two options (reuse at some level vs. build), assess cost, risk, and license fit, then choose.
3. **Refine the design:** follow the sequence of understanding context, confirming architecture, identifying objects, modeling, and specifying interfaces. Expect to loop, and record any backtracking.
4. **Plan the increments:** order them by dependency. Each increment is small enough to verify on its own.
5. **Build each increment test-first:** write the failing test, write minimal code, run, refactor, and update intent notes and the reasoning log.
6. **Reflexion after each increment and at the end:** check against Requirements and Constraints. Look for untraceable code, undocumented assumptions, missing error handling, and interface drift. Revise before moving on.
7. **Close out:** write the configuration and host-target notes, run the full suite from a clean checkout, and compile the deviation list.

### 7. Output Format
Deliver:
1. `README.md`: purpose, setup, how to run, how to test, and the host-target notes
2. `docs/design-rationale.md`: reuse decisions, design models (classes, interfaces, sequence, state), patterns used, intent notes, assumptions, deviations, and open questions
3. `docs/reasoning-log.md`: the prompt and reasoning log
4. `docs/known-issues.md`: the problem-tracking log
5. Source code in a structure that mirrors the architecture's components
6. Tests alongside the code, each commented with the requirement or interface ID it checks
7. `docs/traceability.md`: requirement or decision ID → code and tests
8. A **Handoff Summary for Ch8**: what is built, what is untested or weakly tested, risky areas, interfaces to test at boundaries, and known deviations

### 8. Verification
This is complete when all of the following are true:
- [ ] **Runs clean:** from a clean checkout, following only the README, the build succeeds and all tests pass.
- [ ] **Traceability:** every requirement in scope maps to code and at least one test. No untraceable code exists.
- [ ] **Test-first evidence:** the reasoning log shows tests preceding code for each increment. No increment ends with failing tests.
- [ ] **Interfaces:** each implemented interface matches the Ch6 catalogue and exposes no data representation. A spot check of three boundaries shows both sides agree.
- [ ] **Reuse:** every reuse or build decision is recorded with alternatives considered, and every dependency has a recorded license consistent with `{{reuse_and_license_policy}}`.
- [ ] **Intent documentation:** every module has the what, why, assumptions, and what-breaks-it note. A stranger can state a module's assumptions from the docs alone.
- [ ] **Observability:** an injected failure in one component produces a log or error that identifies the component and the triggering input, and this has been demonstrated.
- [ ] **Deviations:** every departure from the architecture or requirements is listed with its reason and proposed upstream fix.
- [ ] **Scope:** nothing outside `{{build_scope}}` was built, and out-of-scope observations are listed.
- [ ] **Domain-agnostic:** swapping the inputs for an unrelated domain requires changing only the inputs, never this prompt. No unstated domain assumption appears in the output.
- [ ] **Handoff:** the Ch8 summary names weak spots and boundaries to test without requiring a reread of the code.
