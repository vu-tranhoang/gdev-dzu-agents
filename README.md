# gdev-dzu-agents

A reusable AI-assisted game development framework for researching, designing, implementing, reviewing, and learning game development.

The framework is designed to support multiple game projects without containing project-specific game requirements.

> **Framework defines how we work.  
> Project specifications define what we build.**

## Goals

`gdev-dzu-agents` aims to provide a structured AI development team for indie game development.

The framework should help developers:

- research games and real-world domains;
- discover relevant games, mechanics, and hidden gems;
- analyze and design gameplay systems;
- convert game design into technical architecture;
- learn game development while implementing real features;
- implement features from accepted specifications;
- review code and design independently;
- preserve important design and architecture decisions;
- reduce AI hallucination and uncontrolled scope expansion;
- reuse the same development workflow across multiple games.

## Core Concepts

The framework separates four different concepts.

### Instructions

Instructions define global rules governing AI behavior.

They answer:

> **What rules must every AI agent follow?**

Examples:

- authority hierarchy;
- specification compliance;
- research integrity;
- learning rules;
- change control.

Location:

```text
instructions/
```

### Agents

Agents define roles and responsibilities.

They answer:

> **Who is performing the task?**

Examples:

- Game Director
- Game Designer
- Technical Architect
- Developer
- Reviewer
- Learning Coach
- Game Research Analyst
- Game Discovery Scout
- Domain Researcher
- External Design Council

Location:

```text
agents/
```

Agents should orchestrate work and use appropriate skills.

Agents should not duplicate detailed procedures already defined by skills.

### Development Orchestrator

The framework supports a coordination role responsible for routing and continuity across the development workflow.

The Development Orchestrator is not a domain authority that replaces Game Director, Game Designer, Technical Architect, or Reviewer.

Instead, it provides:

- task interpretation;
- routing to the most relevant specialist Agent;
- working context management;
- handoff preparation;
- result consolidation;
- conflict identification;
- escalation when a decision requires higher authority.

The Orchestrator's role is to improve coordination, not to override specialist domain decisions.

Location:

```text
agents/coordination/
```

### Skills

Skills define reusable procedures.

They answer:

> **How should a particular task be performed?**

Examples:

- analyze a reference game;
- discover similar games;
- design a gameplay system;
- design a save system;
- review an implementation;
- create a learning exercise.

Location:

```text
skills/
```

Skills must remain project-agnostic.

A skill must not contain requirements belonging to a specific game.

### Handoff Protocol

The framework includes a Handoff Protocol to pass work between Agents without losing intent, constraints, or authority boundaries.

The Handoff Protocol preserves:

- objective;
- context;
- rationale;
- accepted decisions;
- relevant sources;
- unresolved questions;
- assumptions;
- expected output;
- what may and may not be changed.

Location:

```text
skills/coordination/handoff.md
```

### Project Specifications

Project specifications describe a particular game.

They answer:

> **What are we building?**

Examples:

```text
player movement
career system
economy
world
NPC relationships
property system
quests
```

Project specifications **do not belong in this repository**.

They belong to the repository of the game using this framework.

---

## Repository Structure

```text
gdev-dzu-agents/
│
├── instructions/
│   ├── CONSTITUTION.md
│   ├── AUTHORITY.md
│   └── MODES.md
│
├── agents/
│   ├── coordination/
│   ├── research/
│   ├── design/
│   ├── engineering/
│   ├── quality/
│   └── learning/
│
├── skills/
│   ├── coordination/
│   ├── research/
│   ├── game-design/
│   ├── engineering/
│   ├── development/
│   ├── quality/
│   └── learning/
│
├── workflows/
├── templates/
├── docs/
└── examples/
```

The structure may evolve as the framework matures.

---

## Planned Agent Organization

### Research

- Game Research Analyst
- Game Discovery Scout
- Domain Researcher
- External Design Council

### Design

- Game Director
- Game Designer

### Engineering

- Technical Architect
- Developer

### Quality

- Reviewer

### Learning

- Learning Coach

Agent definitions will be added incrementally.

---

## Authority Principle

AI assists development but does not own the project.

The human project owner remains the final authority.

The expected authority hierarchy is:

```text
Human Project Owner
        ↓
Project Vision
        ↓
Game Pillars
        ↓
Accepted Decisions
        ↓
Accepted Specifications
        ↓
Architecture
        ↓
Current Task
        ↓
Agent Recommendation
```

Lower levels must not silently override higher levels.

Conflicts must be reported rather than automatically resolved.

The workflow model also includes a coordination layer:

```text
Human Project Owner
        |
        v
Development Orchestrator
        |
        +--------------------------+
        |                          |
        v                          v
Specialist Agents            Specialist Agents
```

This coordination layer provides workflow and routing authority, not superior domain authority.

See:

```text
instructions/CONSTITUTION.md
instructions/AUTHORITY.md
```

---

## Conversation History Is Context; Accepted Documents Are Memory

The framework distinguishes between short-term reasoning context and durable project memory.

```text
Conversation history is context.
Accepted documents are memory.
```

Conversation history may help reasoning, but important decisions must eventually be preserved in canonical project documents such as specifications, decision records, architecture notes, and accepted principles.

This prevents the project from depending only on transient AI conversations.

---

## Research Is Not Design

Research findings are evidence, not project requirements.

```text
Research
    ↓
Findings
    ↓
Design Proposal
    ↓
Review / Discussion
    ↓
Human Decision
    ↓
Accepted Specification
```

An interesting mechanic discovered during research must not automatically become part of a game.

---

## AI Development Philosophy

The framework follows several principles:

**Research before assumption.**

**Design before implementation.**

**Specification before production code.**

**Understanding before automation when learning.**

**Review independently from implementation.**

**Prefer simple working systems before unnecessary abstraction.**

**Record why important decisions were made.**

**Preserve intent in handoffs.**

**Treat accepted documents as source-of-truth memory.**

---

## Status

🚧 **Early Development**

Current focus:

1. framework governance;
2. authority model;
3. operating modes;
4. agent contracts;
5. reusable research skills;
6. orchestration and handoff foundations.

No production-ready agent system is available yet.

---

## License

License information is available in `LICENSE`.

