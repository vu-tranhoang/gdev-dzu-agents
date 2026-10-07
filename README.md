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
│   ├── research/
│   ├── design/
│   ├── engineering/
│   ├── quality/
│   └── learning/
│
├── skills/
│   ├── research/
│   ├── game-design/
│   ├── engineering/
│   ├── development/
│   ├── quality/
│   └── learning/
│
├── workflows/
├── templates/
└── docs/
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

See:

```text
instructions/CONSTITUTION.md
instructions/AUTHORITY.md
```

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

---

## Status

🚧 **Early Development**

Current focus:

1. framework governance;
2. authority model;
3. operating modes;
4. agent contracts;
5. reusable research skills.

No production-ready agent system is available yet.

---

## License

License information is available in `LICENSE`.
