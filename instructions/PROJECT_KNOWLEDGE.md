# Project Knowledge Architecture

**Status:** Draft  
**Version:** 0.1

This document defines the intended project-knowledge architecture for downstream game projects built with `gdev-dzu-agents`.

It does not define requirements for this framework repository itself. The framework remains project-agnostic.

---

## 1. Language Policy

### AI-facing / framework-facing artifacts

These should be written in English by default:

- `AGENTS.md`
- files under `instructions/`
- Agent definitions
- Skill definitions
- workflow definitions
- framework rules
- framework templates and machine-facing metadata

These artifacts are primarily consumed repeatedly by AI agents and benefit from consistent technical terminology.

### Project-facing documentation

Documents generated for a specific downstream game project should be written in Vietnamese by default.

Examples:

- project documentation
- Stories
- Requirements
- Analysis
- Design documents
- Test specifications
- research reports
- decision records
- gameplay documentation
- world documentation
- narrative documentation

English technical terms should remain in English when translating them would reduce clarity.

This policy applies to downstream project artifacts, not necessarily to all source code identifiers.

---

## 2. External Reference Use

External repositories and development frameworks may be used as architectural
evidence and inspiration.

They are not sources of truth for this framework.

Use external patterns only when they solve a demonstrated problem in
`gdev-dzu-agents`. Do not copy another repository's workflow, directory
structure, Git strategy, Agent hierarchy, planning format, lifecycle, or
terminology unless it is independently justified by this framework's own goals.

The architecture remains owned by this framework.

---

## 3. Project Structure Concept

A downstream project should conceptually separate:

```text
project/
├── docs/
├── specs/
├── releases/
└── src/
```

These areas have different responsibilities.

---

## 4. `docs/` — Current Project Truth

`docs/` is the consolidated description of the current released project.

It answers:

> What is the project/game now?

`docs/` should be readable as a coherent description of the current released project without forcing the reader to reconstruct history from Stories.

The important semantic rule is:

```text
docs/ != development history

docs/ = consolidated current truth
```

Do not continuously rewrite `docs/` with every Story. Instead, update `docs/` during release documentation review.

---

## 5. `specs/` — Development Record and Traceability

`specs/` represents the historical and working record of how the project evolves.

Conceptually:

```text
specs/
├── vision/
├── epics/
├── stories/
├── decisions/
└── research/
```

This is a conceptual downstream-project structure.

The framework repository itself does not create project-specific directories or game-specific requirements.

Historical project knowledge may be organized by year for readability and
scalability. This applies conceptually to historical EPICs, Stories, Decisions,
and Research records. Year-based organization is a filing strategy, not a
separate authority hierarchy.

---

## 6. Work Item Foundation

The framework uses a minimal Work Item model for downstream project traceability
and scope control. It is not intended to become a Jira clone.

Conceptually:

```text
Project
|
+-- Vision
|
+-- EPIC
|   |
|   +-- Story
|       |
|       +-- Task
|
+-- Decision
|
+-- Research
```

Within an EPIC, the Initial Story and later Stories are siblings:

```text
EPIC
|
+-- Initial Story
+-- Story
+-- Story
+-- Story
    |
    +-- Task
```

Decision and Research artifacts are not required children of a Story. They are
orthogonal project knowledge artifacts.

A Decision or Research artifact may apply to:

- Project;
- EPIC;
- Story;
- architecture or design question;
- technical question;
- another explicitly referenced scope.

References should be preferred over copying full Decision or Research content
inside Stories. This supports context efficiency and keeps authoritative
artifacts in their proper locations.

---

## 7. EPIC Semantics

An EPIC is a bounded initiative at a particular point in the project history.

It is not a permanent category or bucket.

An EPIC should:

- represent a meaningful project goal or initiative;
- establish high-level context;
- establish known scope without inventing unknown scope;
- group related Stories;
- preserve traceability between the initiative and resulting work.

An EPIC is not:

- a permanent category;
- a feature bucket that remains open forever;
- a substitute for detailed requirements;
- a container where AI should automatically generate every imaginable feature.

Every new EPIC should eventually have an Initial Story that captures the
original context and allows analysis before decomposition into additional
Stories.

If analysis reveals another sufficiently large initiative, propose a NEW EPIC instead of silently expanding the current EPIC.

Later related initiatives should normally create a new EPIC and reference the
historical EPICs that provide context. Old EPICs should not become permanent
buckets reopened indefinitely for loosely related work.

---

## 8. Initial Story Semantics

Initial Story is not a separate Work Item type.

It is a normal Story with a special role within a newly created EPIC.

It is normally the first Story used to safely explore, clarify, and establish
the first bounded piece of work before the framework decomposes an EPIC into
additional sibling Stories.

Conceptually:

```text
Idea / Initiative
  >
EPIC
  >
Initial Story
  >
Analysis / Research / clarification
  >
Proposed decomposition
  >
Human Project Owner review
  >
Additional Stories
```

The Initial Story should help discover scope rather than assume scope. This
protects the framework from prematurely inventing requirements or decomposing an
initiative into unapproved features.

Additional Stories created from the Initial Story are siblings under the same
EPIC. They are not children of the Initial Story.

---

## 9. Story Semantics

A Story is the primary traceable unit of development work.

A Story represents one bounded change that can be understood, implemented,
reviewed, and verified independently enough to maintain useful traceability.

Story IDs should be globally sequential within a downstream project. They should
not reset each year, even if Story files are organized into year-based folders.

A downstream project may use a project-specific Story prefix, conceptually:

```text
<PROJECT_PREFIX>-<SEQUENTIAL_ID>
```

This describes the accepted direction for identity semantics. It does not yet
define the full Work Item Standard or a rigid file schema.

A Story may eventually reference or contain concepts such as:

- Story ID;
- parent EPIC;
- goal;
- scope;
- out-of-scope boundaries;
- requirements;
- acceptance criteria;
- dependencies;
- relevant Decisions;
- relevant Research;
- artifacts;
- implementation;
- tests;
- review evidence;
- verification evidence;
- Git traceability.

Do not finalize the Story schema, create Story templates, or finalize filenames
yet. These belong to future Work Item Standard refinement and Story lifecycle
design.

Conceptually, Story-bound work may later produce or reference artifact types
such as:

- requirements;
- analysis;
- design;
- tasks or implementation planning;
- source changes;
- tests;
- review evidence;
- verification evidence.

The exact filenames, schemas, lifecycle states, gates, and transition rules are
not finalized. They belong to the future Work Item Standard.

---

## 10. Story Sizing Principle

A Story should be small enough that:

- its goal is understandable;
- its scope is bounded;
- its acceptance can be evaluated;
- implementation impact can be reasoned about;
- review and verification remain meaningful.

Avoid arbitrary sizing rules such as maximum number of files, maximum number of
Tasks, story points, or fixed development hours.

A Story should be split when it contains independently meaningful changes that:

- can be accepted separately;
- have significantly different risks;
- require different major design decisions;
- have different dependencies;
- make the Story too broad to reason about safely.

Do not force decomposition simply because a Story is technically large. Prefer
semantic boundaries over arbitrary size limits.

---

## 11. Task Semantics

A Task is implementation or planning decomposition within a Story.

Conceptually:

```text
Story
|
+-- Task 01
+-- Task 02
+-- Task 03
+-- Task 04
```

A Task helps describe:

- concrete work;
- execution order;
- dependencies;
- progress;
- optional ownership boundaries.

A Task does not automatically receive the same governance weight as a Story.
By default, a Task does not require:

- its own EPIC relationship;
- its own full lifecycle;
- its own branch;
- its own pull request;
- its own complete requirements document;
- its own full artifact set.

The Story remains the primary traceability and acceptance boundary.

Tasks inherit authority from the Story and its accepted upstream artifacts. A
Task must not silently change:

- Story requirements;
- acceptance criteria;
- accepted design;
- project decisions;
- Story scope.

If executing a Task reveals a contradiction or missing requirement, report a
blocker or unresolved question and return to the Story or appropriate authority.
Implementation Tasks must not become hidden requirement generators.

Optional future Task ownership metadata may help prevent conflicts during
parallel execution:

```yaml
task: <TASK-ID>

depends_on:
  - <TASK-ID>

owns:
  - <resource-reference>
```

Ownership may refer to files, modules, components, or other implementation
resources. It should remain optional. This document does not require ownership
metadata for every Task, implement parallel Agent execution, or create runtime
locking.

Task identity syntax is not finalized. A possible future direction is:

```text
<STORY-ID>-T<SEQUENCE>
```

For example:

```text
SGL-0023-T01
SGL-0023-T02
```

Do not treat this as an accepted Task ID standard. EPIC identity format also
remains deferred.

---

## 12. Concept Separation

The framework must keep these concepts separate:

```text
Agent = WHO performs a responsibility
Skill = HOW a reusable capability is performed
Story / Work Item = WHAT is being changed
Phase = WHERE the work currently is in its execution lifecycle
Mode = HOW MUCH autonomy or interaction style the AI currently has
```

These concepts must not be collapsed into one another.

Learning is not a Story lifecycle phase. A Story should not transition into a
learning state merely because the Human Project Owner wants to understand a
concept, implementation, or trade-off. Learning is orthogonal to lifecycle
progression.

Learning support belongs conceptually under reusable Skills because it changes
how an Agent assists the Human Project Owner. The exact Skill contract is not
designed yet, and no Learning Skill is created by this document.

Learning support is not currently an accepted specialist Agent contract. A
dedicated education-oriented Agent may be introduced later only if justified
through the future Agent Contract design.

Mode is separate from Phase. Phase describes execution lifecycle position, while
Mode should eventually describe interaction and autonomy characteristics such as
AI initiative, Human involvement, explanation depth, and approval expectations.
Mode must not change authority, source of truth, accepted requirements, accepted
scope, or governance. Exact Mode names and contracts are not accepted yet.

Design, implementation, review, and verification are better understood as
possible execution lifecycle concerns than as finalized Modes. Exact lifecycle
states, gates, transitions, and artifact requirements remain deferred to the
future Work Item Standard.

Research remains orthogonal for now. It may occur before a Story exists, for an
EPIC, for a Story, or during analysis/design when evidence is missing. Do not
force Research into Mode, Phase, Agent, or Skill solely for symmetry.

---

## 13. Story-Bound Execution and Traceability

Once work enters Story-bound execution, it should be traceable to a Story ID.

Story is the primary execution, traceability, review, and acceptance boundary.
Tasks decompose execution inside that boundary.

Conceptually, future Story-bound work should support traceability between:

```text
Story ID
  <-> Git branch
  <-> commits
  <-> pull request
  <-> implementation / review / verification evidence
```

Do not treat this as a finalized Git branching strategy. The framework should
prefer the simplest branching strategy that provides sufficient Story
traceability. Git behavior will be specified separately.

Phase transition is not the same thing as a Git commit. A phase may produce
multiple commits.

This does not mean every Story must always produce every possible artifact.
Artifact requirements may depend on Story complexity and future lifecycle rules.

---

## 14. Session-Based Execution

The framework is intended to support solo developers, very small teams, and
Human-directed AI-assisted development.

Different responsibilities may be performed in separate AI sessions. The
framework must not require those sessions to share conversation history.

Conceptually:

```text
Human Project Owner
  >
AI Session A
Agent / Role A
  >
Output Artifact
  >
Human reviews / refines
  >
AI Session B
Agent / Role B
  >
Next Output Artifact
```

Accepted project artifacts provide continuity between sessions.

This reinforces the memory principle:

```text
Conversation history is context.
Accepted documents are memory.
```

Each session should be able to reconstruct the minimum necessary working context
from canonical repository artifacts.

---

## 15. Artifact-Driven Progression

Execution phases should eventually produce explicit outputs. After acceptance,
an earlier phase output may become an authoritative input to later work.

Artifacts are the primary durable interface between development sessions.

An upstream session produces an artifact. A downstream session consumes that
artifact as authoritative input within its accepted scope.

Conceptually:

```text
Phase A
  >
Artifact A
  >
Phase B
  >
Artifact B
```

Artifacts reduce dependency on conversation history, hidden Agent memory,
long-running sessions, and autonomous orchestration.

Artifacts should preserve the information necessary for downstream work without
copying unnecessary context. References to canonical Decisions, Research,
requirements, and dependencies should be preferred over duplicating their full
contents.

Conceptual phase output examples:

```text
analysis produces analysis output
design produces accepted design output
planning produces implementation plan or tasks
implementation produces code, tests, and implementation evidence
review produces review findings or result
verification produces acceptance evidence or result
```

This is conceptual architecture guidance only. It does not finalize lifecycle
states, artifact schemas, filenames, gates, or transitions.

---

## 16. Human-Directed Progression

Do not introduce a formal Gate subsystem at this stage.

For the intended solo and small-team workflow, the Human Project Owner controls
progression.

Conceptually:

```text
Current Phase
  >
Agent produces output
  >
Human reviews
  >
refine current output OR proceed to next Phase
```

If the Human Project Owner is not satisfied, refine the current output and
remain in the current Phase. Do not create a new Story status merely to
represent revision.

If the Human Project Owner intentionally starts the next Phase using the
upstream output, that action conceptually means the upstream output is accepted
enough to continue development.

Do not require approval machinery such as gate records, approval databases, or
approval metadata. Formal approval metadata may be reconsidered later only if a
larger-team use case demonstrates a real need.

---

## 17. Blockers and Story Status

Do not create a Story Status state machine in this framework foundation.

The document statuses defined by the Authority Model, such as Draft, Review,
Accepted, Deprecated, and Superseded, describe document authority/status. They
must not be automatically reinterpreted as Story statuses.

If work cannot safely continue because information or authority is missing,
represent the problem conceptually as a blocker, unresolved question, conflict,
or required decision.

After resolution, work continues in the appropriate current Phase. A blocker is
a condition affecting execution, not necessarily the identity or lifecycle
status of the Story.

---

## 18. Phase Direction

Story describes what is changing.

Phase describes where that Story currently is in execution.

Do not finalize the complete Phase lifecycle yet.

The architecture is moving toward a lightweight future Phase Contract based on:

```text
Phase
|-- Purpose
|-- Responsible Agent / Role
|-- Required Inputs
|-- Expected Outputs
|-- Authority Boundaries
+-- Completion Meaning
```

This is the intended next design problem. This document does not create the
final Phase Contract, finalize exact Phase names, or define transitions, gates,
entry criteria, exit criteria, or required artifacts.

Future Phase design should prefer:

```text
Required Inputs
  >
Responsible Agent / Role
  >
Work
  >
Expected Output Artifact
  >
Human review / refinement
  >
Next Phase
```

over a complex workflow state machine.

---

## 19. Runtime Independence

A framework Agent is a role and responsibility contract. It is not necessarily
the same thing as a runtime-specific AI Agent implementation.

Conceptually:

```text
Framework Agent
  =
WHO is responsible
+ authority boundaries
+ expected responsibility
```

A framework Agent may eventually be executed through a dedicated AI chat/session,
a Codex session, a Codex subagent, another AI coding tool, or a future
orchestration runtime.

The core framework must remain runtime-independent:

```text
Framework core:
  Story / Work Item
  Phase
  Agent Contract
  Skills
  Inputs
  Outputs / Artifacts

Runtime adapter:
  Codex
  Claude
  Cursor
  Agents API
  Future runtime
```

The framework defines development semantics. Runtime adapters define how those
semantics are exposed to a particular AI tool.

OpenAI Codex is currently the primary runtime used while developing and
dogfooding this framework. Codex-specific invocation mechanics must not define
the core framework architecture. Future Codex integration belongs to a future
adapter or integration layer.

Do not move framework `skills/` merely to match runtime-specific discovery
conventions. Skills remain reusable framework capabilities. Future runtime
adapters may expose or map framework Skills into runtime-native mechanisms, but
that mapping is not designed here.

---

## 20. Releases

The conceptual role of `releases/` should exist.

A Release groups completed and accepted work into a deliverable project version.

Do not force a one-to-one relationship between Release and EPIC.

A Release may include work from multiple EPICs.

Story completion does not directly rewrite `docs/`.

Release documentation consolidation is the point where affected `docs/` should
be updated to reflect accepted completed work. This keeps `docs/` focused on
current released truth rather than development history.

The framework may later define a Release Documentation Curator role to handle
this consolidation responsibility. That role is conceptual only and is not
created by this document.

---

## 21. Future Audit and Context Responsibilities

The framework may later define a Project Auditor role to review consistency
between accepted decisions, specifications, release documentation, and current
project truth. That role is conceptual only and is not created by this document.

Context scope should eventually become an explicit responsibility in Agent
contracts. Until those contracts are designed, agents should continue to follow
the general principle of reading the minimum authoritative context required to
perform the current task safely.

---

## 22. Three Different Forms of Project Truth

The project should distinguish between:

```text
specs/ = historical development record,
  rationale,
  evidence,
  requirements,
  analysis,
  design,
  traceability

docs/  = consolidated description
  of the current released project

src/   = executable implementation
```

Another useful summary:

```text
specs/ = WHY / HOW WE GOT HERE

docs/  = WHAT THE PROJECT IS NOW

src/   = WHAT THE SOFTWARE DOES
```

These sources must not be treated as interchangeable.

---

## 23. Context Efficiency / Token Policy

AI agents must not read the entire repository by default.

The framework principle is:

> Read the minimum authoritative context required to perform the current task safely.

and:

> Agents should navigate by references, not by repository-wide reading.

Context expansion should normally require at least one justified reason:

1. dependency;
2. authority;
3. conflict;
4. missing information.

---

## 24. Progressive Context Disclosure

A conceptual context-loading model:

```text
Layer 0
AGENTS.md

    ↓

Layer 1
Relevant Agent Contract

    ↓

Layer 2
Relevant Skill

    ↓

Layer 3
Current Story / Work Item

    ↓

Layer 4
Explicitly referenced
Decision / Research / Docs / Dependencies

    ↓

Layer 5
Relevant source code
```

This is conceptual guidance, not a rigid implementation algorithm.

Agents working on one Story should not automatically read every Story, EPIC, Decision, or Research file in the project.

Separate sessions should not require full history from previous sessions. Read
only what is necessary for the current responsibility.

---

## 25. Reference-Driven Context

Future Story/work-item formats should support explicit references such as:

```yaml
epic: <EPIC-ID>

depends_on:
  - <STORY-ID>

decisions:
  - <DECISION-ID>

research:
  - <RESEARCH-ID>

affected_docs:
  - <document-reference>
```

The purpose is to allow agents to follow explicit relationships instead of scanning the repository.

The Work Item model should support progressive context disclosure. An Agent
working on one Story should normally be able to navigate:

```text
Current Story
  >
Parent EPIC
  >
Explicit dependencies
  >
Referenced Decisions
  >
Referenced Research
  >
Relevant source code
```

Work Item relationships should reduce context usage rather than increase it.

---

## 26. Handoff and Context Efficiency

The Handoff Skill must follow this principle:

> Preserve necessary context, not maximum context.

A Handoff should preserve:

- objective;
- current task;
- relevant context;
- accepted decisions;
- rationale;
- constraints;
- assumptions;
- unresolved questions;
- progress;
- expected output;
- authority boundaries;
- canonical references.

It should prefer referencing authoritative artifacts instead of copying their full contents.

Artifacts provide durable project continuity. Handoff provides focused
responsibility-transfer context when additional information is needed.

```text
Artifact = durable project knowledge / output
Handoff = focused responsibility-transfer context
```

Separate AI sessions do not automatically require a large Handoff if the
necessary context is already recoverable from canonical artifacts.

---

## 27. Architecture Minimalism

Before adding any new mechanism, ask:

> What problem does this solve that the current framework cannot solve?

Prefer simple, explicit, traceable, Human-directed, artifact-driven, and
runtime-independent architecture over autonomous, state-heavy, workflow-heavy,
or runtime-coupled mechanisms unless future requirements demonstrate the need.

---

## 28. Summary

The central principles are:

```text
Framework is reusable.
Project knowledge is downstream.

specs/ = historical record and traceability

docs/  = current released truth

src/   = executable implementation
```

Agents should operate with minimal necessary context, follow explicit references, and resolve conflicts using authority before silently choosing a source.

This preserves accuracy, scalability, and traceability without turning the framework into project-specific logic.
