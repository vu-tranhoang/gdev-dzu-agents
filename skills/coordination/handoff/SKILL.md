---
name: agent-handoff
description: >
  Transfer work from one AI agent or development role to another while preserving
  objective, accepted decisions, rationale, constraints, unresolved questions, authority
  boundaries, current progress, and canonical source references. Use when responsibility
  for an active task moves between agents or specialist roles. Ensures receiving agent
  understands both WHAT must be done and WHY it matters. Prevents loss of context,
  silent reinterpretation of requirements, or unauthorized scope expansion.
---

# Agent Handoff Skill

**Version:** 0.1  
**Status:** Active

The Handoff Skill defines how one Agent transfers work to another Agent without losing intent, constraints, or authority boundaries.

Handoff is NOT simple summarization.

Its purpose is to preserve both **WHAT** and **WHY** so the receiving Agent can work safely and effectively.

---

## When to Use Handoff

Use Handoff when:

- responsibility for a task moves from one role to another;
- work transfers between Agents with different expertise;
- continuity and context preservation are important;
- the receiving Agent needs to understand not just the task but its rationale.

Do NOT use Handoff for:

- simple status updates;
- casual reference between Agents;
- routine task assignments without context.

---

## What Handoff Preserves

Handoff must preserve:

1. **Objective** — what needs to be achieved;
2. **Rationale** — why this work is important;
3. **Accepted Decisions** — what is already decided and cannot change;
4. **Constraints** — boundaries that must be respected;
5. **Assumptions** — what is assumed but not yet confirmed;
6. **Unresolved Questions** — what is still unknown;
7. **Current Progress** — what has been completed;
8. **Remaining Work** — what still needs to happen;
9. **Expected Output** — what the receiving Agent should produce;
10. **Authority Boundaries** — what the receiving Agent may and may not modify;
11. **Canonical Sources** — references to authoritative documents.

---

## Handoff Structure

Use this structure when transferring work:

```yaml
handoff:

  from:
    agent: <source-role>
    reason: why responsibility is transferring

  to:
    agent: <target-role>
    why-this-agent: why this agent is appropriate for the next phase

  task:
    title: <task-title>
    type: research | design | architecture | implementation | review | learning

  objective:
    primary: >-
      What needs to be achieved.
    success_criteria:
      - criterion 1
      - criterion 2

  context:
    summary: >
      Minimum context required by receiving agent to understand the work.
      Keep concise. Reference canonical documents for detailed information.
    background: >
      How did we get here? What decisions led to this point?

  rationale:
    - Why this work exists
    - Why the current approach was chosen
    - What problem this solves
    - What happens if work is not completed

  accepted_decisions:
    - decision 1
    - decision 2
    - Note: These CANNOT be changed without higher authority approval.

  constraints:
    - constraint 1
    - constraint 2
    - Note: These define boundaries the receiving agent must respect.

  assumptions:
    - assumption 1 (marked as assumption, not fact)
    - assumption 2
    - Note: If an assumption proves wrong, report it immediately.

  relevant_sources:
    canonical_docs:
      - docs/specs/system/system-spec.md
      - docs/decisions/DEC-001-architecture.md
      - instructions/AUTHORITY.md
    research_findings:
      - research/game-analysis.md
    project_references:
      - project/vision.md

  progress:
    completed:
      - item 1
      - item 2
    in_progress:
      - item 3
    remaining:
      - item 4
      - item 5

  unresolved_questions:
    - question 1 (open for investigation)
    - question 2 (waiting for owner decision)
    - Note: Do not convert these into assumptions without marking the change.

  expected_output:
    primary:
      - deliverable 1
      - deliverable 2
    format: markdown | code | decision-record | specification
    review_criteria:
      - compliance with specification
      - architectural consistency
      - edge case coverage

  authority:
    may_modify:
      - implementation details
      - recommended approaches
      - supporting documentation
    may_not_modify:
      - accepted specification
      - game pillars
      - project vision
      - accepted architecture decisions
    requires_approval_for:
      - scope expansion
      - requirement changes
      - architectural modifications

  blockers:
    - blocker 1 (if any exist)
    - Note: Receiving agent should NOT proceed if blockers prevent safe work.

  previous_attempts:
    if_relevant: >
      What has already been tried? What did not work?
      Why was the previous approach abandoned?
```

Not every field is required for every Handoff.

Include fields relevant to the specific work and receiving Agent.

---

## Handoff Rules

### Rule 1: No Silent Reinterpretation

The receiving Agent must not silently reinterpret accepted decisions.

If an accepted decision appears to conflict with the current task:

1. Report the conflict.
2. Do not proceed silently.
3. Escalate if necessary.

### Rule 2: Canonical Sources Have Priority

If Handoff text conflicts with an accepted canonical document:

1. Identify which source has higher authority.
2. Report the conflict.
3. Do not silently choose the Handoff text.
4. Escalate if necessary.

**Canonical documents always have priority over conversation history or Handoff summaries.**

### Rule 3: Preserve Unresolved Questions

Unknown information must remain explicitly unknown.

Do not convert unresolved questions into assumptions without marking the change.

If the receiving Agent discovers new information, report it explicitly.

### Rule 4: Preserve Assumptions

Assumptions must remain labeled as assumptions.

Do not present assumptions as confirmed facts.

If an assumption proves incorrect during work, report it immediately.

### Rule 5: Preserve Rationale

Important decisions must preserve both WHAT and WHY.

The receiving Agent should understand:

- What was decided;
- Why it was decided;
- What alternatives were considered;
- What problem it solves.

### Rule 6: Preserve Authority Boundaries

The Handoff must clearly communicate:

- What the receiving Agent may modify;
- What the receiving Agent may NOT modify;
- What requires approval from higher authority.

### Rule 7: Avoid Context Dumping

Do not copy entire conversation histories when:

- Canonical references plus concise context are sufficient;
- The conversation contains tangential discussion;
- Important points are already documented.

Reference canonical sources instead.

### Rule 8: Escalate Missing Authority

If completing the task requires a decision outside the receiving Agent's authority:

1. Create an explicit blocker.
2. Do not ask the Agent to invent the decision.
3. Do not leave authority boundaries ambiguous.
4. Escalate to the proper authority (owner, Game Director, Technical Architect, etc.).

---

## Blocker Format

When work is blocked by missing authority, use this format:

```yaml
blocker:

  discovered_by:
    agent: <role-that-found-it>

  issue:
    title: <brief-title>
    description: >
      What is preventing work from continuing safely?

  affected_systems:
    - system 1
    - system 2

  reason:
    why_work_cannot_continue: >
      Implementation cannot safely proceed because...

  required_decision:
    what_must_be_decided: >
      What decision is needed to unblock this?

  required_authority:
    roles:
      - game-director
      - technical-architect
      - human-owner
    reason: "Only these roles have authority to decide this."

  suggested_options: (optional)
    option_a: description
    option_b: description

  status: unresolved
  created_at: <timestamp>
```

---

## Example: Good Handoff

```yaml
handoff:

  from:
    agent: game-designer
    reason: Design phase complete, architecture design needed

  to:
    agent: technical-architect
    why-this-agent: Architecture design is Technical Architect's domain

  task:
    title: Design technical architecture for property system
    type: architecture

  objective:
    primary: Convert accepted gameplay design into a performant, maintainable technical architecture.
    success_criteria:
      - Identifies all required systems and their interactions
      - Proposes data structures and algorithms
      - Identifies performance risks and proposes mitigations
      - References relevant architecture patterns

  context:
    summary: >
      Property system allows players to own and manage properties.
      Properties can be affected by world events. Players should have opportunities to react.
    background: >
      Gameplay design completed and accepted. Property mechanics focus on player agency
      and avoiding invisible negative consequences.

  rationale:
    - "Major world events should provide information signals before significant impact."
    - "Player agency requires notification and response opportunities."
    - "System must support hundreds of properties without performance degradation."

  accepted_decisions:
    - Property values change due to world events (ACCEPTED - no override)
    - Players must have advance warning of major impacts (ACCEPTED - no override)
    - Property system must integrate with economy system (ACCEPTED - no override)

  constraints:
    - Do not redesign the economy system
    - Do not introduce unavoidable random property loss
    - Architecture must support save/load functionality

  assumptions:
    - Property update frequency can be decoupled from frame rate
    - World events are managed by a separate system
    - Player notifications use existing UI system

  relevant_sources:
    canonical_docs:
      - docs/specs/property/property-system.md
      - docs/specs/world/world-events.md
      - docs/decisions/DEC-014-information-signals.md
      - architecture/economy-architecture.md

  progress:
    completed:
      - Gameplay mechanics defined and accepted
      - Player experience requirements documented
      - Integration points with economy identified
    remaining:
      - Technical architecture
      - Data structure design
      - Performance analysis

  unresolved_questions:
    - How frequently should property values be recalculated?
    - Should property changes be saved to disk immediately or batched?
    - How should property state synchronize across save/load boundaries?

  expected_output:
    primary:
      - Architecture proposal
      - Data structure recommendations
      - Performance risk analysis
      - Integration points documentation
    format: markdown specification with diagrams

  authority:
    may_modify:
      - technical implementation approach
      - data structures and algorithms
      - performance optimizations
    may_not_modify:
      - accepted property mechanics
      - requirement for advance warnings
      - integration with economy system
    requires_approval_for:
      - changes to player-facing behavior
      - impact on other systems
      - save/load format changes
```

---

## Example: Bad Handoff

❌ **DO NOT DO THIS:**

```yaml
handoff:
  from: game-designer
  to: technical-architect
  task: Design architecture for property system
  context: >
    The player owns property. Property values change due to world
    events. Players need to know about this. Use component-based
    architecture because it's more flexible.
```

**Problems:**

- No rationale (why does the architecture need to be component-based?);
- No accepted decisions (what has already been decided?);
- No constraints (what cannot change?);
- No unresolved questions (what is still uncertain?);
- No authority boundaries (what can the architect change?);
- Vague context ("players need to know" — what does that mean exactly?);
- No reference to canonical sources;
- No blocker format if issues arise.

---

## Using Handoff in Practice

### Step 1: Identify When Handoff Is Needed

When responsibility moves between Agents or roles, use Handoff.

### Step 2: Gather Information

Collect:

- objective and success criteria;
- rationale for the work;
- accepted decisions and constraints;
- assumptions and unresolved questions;
- references to canonical documents;
- current progress and remaining work.

### Step 3: Prepare the Handoff Document

Use the structure provided above.

Include only fields relevant to this specific Handoff.

Do not over-document trivial work.

### Step 4: Review Before Transfer

Before sending Handoff to the receiving Agent:

- Verify canonical documents are referenced, not duplicated;
- Confirm authority boundaries are clear;
- Ensure assumptions are labeled as assumptions;
- Check that unresolved questions are not hidden;
- Verify no silent reinterpretation of accepted decisions.

### Step 5: Transfer and Confirm Understanding

Send Handoff to receiving Agent.

Confirm they understand:

- what they are expected to do;
- why it matters;
- what they cannot change;
- what authorities block their work (if any).

---

## References

- Authority hierarchy: `instructions/AUTHORITY.md`
- Constitutional rules: `instructions/CONSTITUTION.md`
- Development Orchestrator: `agents/coordination/orchestrator.md`
