---
name: streamline
description: Simplify and right-size technical plans, architectures, workflows, or implementations. Use when the user asks to reduce complexity, remove overengineering, consolidate moving parts, or find the smallest maintainable design that meets current requirements.
---

# Streamline

Reduce the target artifact to the smallest maintainable design that satisfies
the user's current requirements. Deliver a revised artifact alongside any
critique. Preserve the user's intent, scope, and authorization boundaries.

## Establish the contract

Identify the required outcome, explicit constraints, acceptance criteria, and
material risks. Separate current requirements and observed failure modes from
speculative future needs.

Inventory the design's meaningful moving parts at a level proportional to the
task. Include services, processes, state stores, scheduled jobs, secrets,
rollout phases, abstractions, and operational procedures when present.

Each moving part needs a clear connection to one of these grounds:

- a current requirement or acceptance criterion;
- an observed failure mode;
- a security, correctness, durability, or operational constraint.

Consolidate, remove, or defer parts without such a connection. Prefer designs
with fewer ownership boundaries, state transitions, failure modes, and
coordination paths. File count and line count are weak proxies for complexity;
use the system's behavior and operating burden as the primary measures.

## Revise the artifact

Produce the simplified version in the form the user needs. Edit authorized
files for an implementation request. For a review or planning request, provide
a replacement plan, architecture, workflow, or code sketch that can be used
directly.

The revision must retain applicable:

- security, trust, and permission boundaries;
- correctness and data-durability guarantees;
- destructive-action safeguards and recovery paths;
- explicit acceptance criteria;
- compatibility and operational constraints.

Use the simplest design that preserves these properties. A smaller component
count must preserve every required guarantee. Keep redundancy when it serves a
named failure domain or recovery requirement.

When the artifact is already right-sized, return it in the requested form and
explain how each remaining part supports the contract. Preserve any deferred
additions and their triggers.

## Explain the result

Alongside the revised artifact, identify:

- complexity removed or consolidated;
- constraints and safeguards retained;
- deferred additions, each paired with a measurable trigger for reconsidering
  it.

Omit the deferred list when no additions are being deferred. Keep this
explanation shorter than the revised artifact unless the user asks for a full
design analysis.
