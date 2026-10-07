---
name: agent-handoff
description: Use when transferring work between Agents or roles so the receiving role gets the objective, rationale, constraints, authority boundaries, unresolved questions, and canonical source references without copying unnecessary context.
---

# Agent Handoff

Use this Skill when responsibility for work moves from one Agent or role to
another.

The goal is to preserve necessary context, not maximum context. Prefer concise
summaries plus canonical source references over copying full document contents
or conversation history.

## Authority

Canonical accepted documents outrank Handoff summaries. If a Handoff conflicts
with an accepted canonical document, surface the conflict and follow the
authority hierarchy instead of silently resolving it.

Handoffs do not grant new domain authority. The receiving role may only make
decisions within its accepted authority boundaries.

## Handoff Content

Include:

- source role and reason for transfer;
- target role and reason it is appropriate;
- objective;
- rationale;
- relevant accepted decisions;
- constraints and non-goals;
- assumptions;
- unresolved questions or blockers;
- progress already completed;
- expected output;
- acceptance or review expectations;
- authority boundaries;
- canonical source references.

## Format

Use a compact structured format when possible:

```yaml
from:
  role: <source-role>
  reason: <why work is moving>

to:
  role: <target-role>
  reason: <why this role fits>

objective: <what must be achieved>

rationale: <why this work matters>

context:
  accepted_decisions:
    - <decision or reference>
  constraints:
    - <constraint>
  assumptions:
    - <assumption>
  unresolved_questions:
    - <question or blocker>

progress:
  completed:
    - <completed item>
  remaining:
    - <remaining item>

expected_output:
  deliverable: <expected deliverable>
  review_expectations:
    - <acceptance or review expectation>

authority:
  may_modify:
    - <allowed area>
  may_not_modify:
    - <protected area>
  requires_approval:
    - <decision requiring approval>

canonical_sources:
  - <path or accepted document reference>
```

## Rules

- Do not silently reinterpret accepted decisions.
- Do not copy whole canonical documents unless the receiving role needs the
  full content and no stable reference is sufficient.
- Preserve known uncertainty as uncertainty.
- Escalate when the receiving role would need a decision outside its authority.
