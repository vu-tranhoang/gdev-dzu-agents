# Codex Repository Instructions for gdev-dzu-agents

**Status:** Active  
**Version:** 0.1  
**Runtime:** OpenAI Codex (primary)

This repository defines a reusable AI-assisted game development framework.

It contains:

- governance rules;
- AI Agent role definitions;
- reusable Skills;
- workflows;
- templates.

It does **NOT** contain requirements for a specific game.

---

## Core Rules

### 1. Human Authority

The Human Project Owner has final authority over the project.

You may analyze, research, propose, challenge, and review.

You must not assume ownership of project decisions.

### 2. Read and Respect Governance

Before making significant framework changes, read the relevant governance and authority files.

Relevant references:

- `instructions/CONSTITUTION.md`
- `instructions/AUTHORITY.md`
- `instructions/PROJECT_KNOWLEDGE.md`

### 3. Canonical Documents Have Priority

Accepted canonical documents have higher authority than:

- conversation history;
- agent recommendations;
- temporary summaries.

If a conflict exists between this message and an accepted canonical document:

1. identify the conflict;
2. report it;
3. escalate if necessary.

### 4. Language Policy

Use the framework-level language convention:

- English by default for AI-facing framework artifacts: `AGENTS.md`, `instructions/`, agent definitions, skill definitions, workflow definitions, framework templates, metadata.
- Vietnamese by default for downstream project-facing documentation: stories, requirements, analysis, design docs, research notes, decision records, gameplay/world/narrative documentation.
- Preserve technical English terms when translating would reduce clarity.

### 5. Research Is Evidence, Not Decision

Research findings are evidence, not project requirements.

### 6. Do Not Silently Create Requirements

Do not:

- invent missing requirements;
- expand scope without approval;
- silently modify accepted specifications, decisions, or governance.

Report blockers instead.

### 7. Preserve Both WHAT and WHY

When decisions matter, preserve both:

- **WHAT** was decided;
- **WHY** it was decided.

### 8. Use Appropriate Specialist Roles

Do not allow one Agent to perform every responsibility.

Route tasks to the appropriate specialist role when available.

### 9. Use Handoff When Responsibility Moves

When work transfers between Agents or roles, use the `agent-handoff` Skill.

Preserve objective, rationale, accepted decisions, constraints, assumptions, unresolved questions, authority boundaries, and canonical source references.

### 10. Prefer Simplicity Over Abstraction

Favor understandable working solutions.

Avoid unnecessary frameworks, abstraction layers, design patterns, or infrastructure unless they solve a demonstrated problem.

---

## Memory Principle

```text
Conversation history is context.
Accepted documents are memory.
```

Important project knowledge must eventually exist in canonical repository documents such as:

- accepted specifications;
- decision records;
- architecture notes;
- project vision;
- game pillars.

This repository and its accepted documents are the long-term source of truth.

Conversation history supports reasoning but is not permanent project memory.

---

## Project Knowledge Architecture

The framework remains project-agnostic.

A downstream game project may conceptually separate:

```text
project/
├── docs/
├── specs/
├── releases/
└── src/
```

Key distinction:

```text
specs/ = historical development record, rationale, evidence, analysis, traceability

docs/  = consolidated current truth of the released project

src/   = executable implementation
```

Do not treat these as interchangeable.

---

## Context Efficiency

Agents must follow:

> Read the minimum authoritative context required to perform the current task safely.

and:

> Agents should navigate by references, not by repository-wide reading.

Context expansion should normally require a justified reason:

1. dependency;
2. authority;
3. conflict;
4. missing information.

Do not read the entire repository by default.

---

## Progressive Disclosure

Do NOT read every file before every task.

Instead, read conditionally:

### When changing governance

Read relevant files under `instructions/`.

### When acting in a defined role

Read the corresponding role definition under `agents/`.

### When a task matches an available Skill

Use the relevant Skill under `skills/`.

### When implementing from a project specification

Read the relevant specification and accepted decisions first.

---

## Framework Structure

```text
instructions/
  ├── CONSTITUTION.md
  ├── AUTHORITY.md
  └── PROJECT_KNOWLEDGE.md

agents/
  ├── coordination/
  │   └── orchestrator.md
  ├── design/
  ├── engineering/
  ├── learning/
  ├── quality/
  └── research/

skills/
  ├── coordination/
  │   └── handoff/
  │       └── SKILL.md
  ├── development/
  ├── engineering/
  ├── game-design/
  ├── learning/
  ├── quality/
  └── research/

workflows/
templates/
examples/
```

---

## Agent vs Skill

**Agent = WHO**

Defines roles and responsibilities.

Example: `Development Orchestrator`

**Skill = HOW**

Defines reusable procedures.

Example: `agent-handoff`

Agents may use Skills. Multiple Agents may use the same Skill.

---

## Development Orchestrator

Location: `agents/coordination/orchestrator.md`

The Orchestrator is a coordination role, not a domain authority.

It has **Workflow Authority** over:

- task routing;
- task classification;
- Handoff preparation;
- context management;
- result consolidation;
- blocker identification;
- escalation.

It does NOT have **Domain Authority** over:

- game direction;
- game design;
- technical architecture;
- implementation;
- review.

Specialist Agents retain their respective domain responsibilities.

---

## Getting Started

### For governance questions

Read:

- `instructions/CONSTITUTION.md` — fundamental rules;
- `instructions/AUTHORITY.md` — authority hierarchy and role definitions;
- `instructions/PROJECT_KNOWLEDGE.md` — project knowledge and context policy.

### For coordination work

Use:

- `agents/coordination/orchestrator.md` — Orchestrator role definition;
- `skills/coordination/handoff/SKILL.md` — Handoff Skill for transferring work between Agents.

---

## Important

This repository is a **framework**, not a game project.

Do not introduce:

- game-specific story, lore, or characters;
- engine-specific code or configuration;
- project-specific economy, maps, or mechanics;
- runtime implementation (Python, JavaScript, MCP, etc.);
- persistent project state storage.

Extensions and integrations belong in the game project repository, not here.

---

## References

- Full governance: `instructions/CONSTITUTION.md`, `instructions/AUTHORITY.md`
- Project knowledge and context policy: `instructions/PROJECT_KNOWLEDGE.md`
- Security policy: `SECURITY.md`
- Repository overview: `README.md`, `README-vn.md`
