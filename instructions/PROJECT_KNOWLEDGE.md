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

The core Work Item hierarchy is:

```text
EPIC
  >
Initial Story
  >
Story
  >
Task
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

Its purpose is to safely explore, analyze, clarify, and establish the first
bounded piece of work before the framework decomposes an EPIC into additional
Stories.

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

## 14. Artifact-Driven Progression

Execution phases should eventually produce explicit outputs. After acceptance,
an earlier phase output may become an authoritative input to later work.

Conceptually:

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

## 15. Releases

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

## 16. Future Audit and Context Responsibilities

The framework may later define a Project Auditor role to review consistency
between accepted decisions, specifications, release documentation, and current
project truth. That role is conceptual only and is not created by this document.

Context scope should eventually become an explicit responsibility in Agent
contracts. Until those contracts are designed, agents should continue to follow
the general principle of reading the minimum authoritative context required to
perform the current task safely.

---

## 17. Three Different Forms of Project Truth

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

## 18. Context Efficiency / Token Policy

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

## 19. Progressive Context Disclosure

A conceptual context-loading model:

```text
Layer 0
AGENTS.md

    ↓

Layer 1
Relevant Agent definition

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

---

## 20. Reference-Driven Context

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

## 21. Handoff and Context Efficiency

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

---

## 22. Summary

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
