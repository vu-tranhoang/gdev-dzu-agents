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

## 2. Project Structure Concept

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

## 3. `docs/` — Current Project Truth

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

## 4. `specs/` — Development Record and Traceability

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

---

## 5. EPIC Semantics

An EPIC is a bounded initiative at a particular point in the project history.

It is not a permanent category or bucket.

Every new EPIC should eventually have an Initial Story that captures the original context and allows analysis before decomposition into additional Stories.

If analysis reveals another sufficiently large initiative, propose a NEW EPIC instead of silently expanding the current EPIC.

---

## 6. Story Artifact Model

A Story is the primary traceable unit of development work.

Conceptually, a Story may contain:

```text
<STORY-ID>/
├── STORY.md
├── REQUIREMENTS.md
├── ANALYSIS.md
├── DESIGN.md
├── TASKS.md
└── TESTS.md
```

The exact schema may evolve, but the purpose is to preserve traceability from requirement to implementation.

---

## 7. Releases

The conceptual role of `releases/` should exist.

A Release groups completed and accepted work into a deliverable project version.

Do not force a one-to-one relationship between Release and EPIC.

A Release may include work from multiple EPICs.

---

## 8. Three Different Forms of Project Truth

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

## 9. Context Efficiency / Token Policy

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

## 10. Progressive Context Disclosure

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

Agents working on one Story should not automatically read every Story, EPIC, or research file in the project.

---

## 11. Reference-Driven Context

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

---

## 12. Handoff and Context Efficiency

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

## 13. Summary

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
