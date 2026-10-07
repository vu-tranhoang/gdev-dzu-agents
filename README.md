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

---

## Project Knowledge Architecture

The framework remains project-agnostic. A downstream game project may use the following conceptual structure:

```text
project/
├── docs/
├── specs/
├── releases/
└── src/
```

The intended distinction is:

```text
specs/ = historical development record, rationale, evidence, design, and traceability

docs/  = consolidated current truth of the released project

src/   = executable implementation
```

This separation avoids mixing historical development notes with the current project state.

A project should not treat `docs/`, `specs/`, and `src/` as interchangeable documents.

---

## Repository Structure

```text
gdev-dzu-agents/
│
├── instructions/
│   ├── CONSTITUTION.md
│   ├── AUTHORITY.md
│   └── PROJECT_KNOWLEDGE.md
│
├── agents/
│   ├── coordination/
│   │   └── orchestrator.md
│   ├── design/
│   ├── engineering/
│   ├── learning/
│   ├── quality/
│   └── research/
│
├── skills/
│   ├── coordination/
│   │   └── handoff/
│   │       └── SKILL.md
│   ├── development/
│   ├── engineering/
│   ├── game-design/
│   ├── learning/
│   ├── quality/
│   └── research/
│
├── workflows/
├── templates/
├── examples/
├── README.md
├── README-vn.md
├── SECURITY.md
└── AGENTS.md
```

---

## Context Efficiency

Agents should follow:

> Read the minimum authoritative context required to perform the current task safely.

and:

> Navigate by references instead of reading the repository broadly.

Context expansion should only happen when there is a justified reason, such as:

- dependency;
- authority;
- conflict; or
- missing information.

This keeps the framework scalable and avoids mixing current project truth with stale historical findings.

---

## Security

See `SECURITY.md` for repository security constraints.

---

## License

License information is available in `LICENSE`.
