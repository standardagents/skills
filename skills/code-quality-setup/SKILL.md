---
name: code-quality-setup
description: Set up repository code-quality rules and stack-appropriate enforcement rails. Use when the user asks to establish quality standards, add quality infrastructure, or invokes $code-quality-setup. The skill adds documentation and guardrails without modifying application code.
---

# Code Quality Setup

Lay the rails that future engineering work will follow. Add a clear quality
contract and connect the repository's native tools to it. Leave application
quality work for later tasks.

Read [the shared standards](references/standards.md) before setup. Read [the
dmux-rs example](references/dmux-rs.md) when the repository needs a concrete
calibration for setup scope.

## Boundary

This skill may change:

- `AGENTS.md`, `CLAUDE.md` symlinks, and dedicated quality documentation;
- formatter, linter, type-checker, and source-limit configuration;
- quality check scripts and dedicated enforcement code;
- CI, release, and build wiring that invokes those checks.

Do not change application source, application tests, fixtures, snapshots, or
product behavior. Do not fix findings, format application files, refactor,
rename, reorganize, or add tests. Do not inventory or classify existing debt.

Preserve unrelated working-tree changes. Stop and restore only the skill's
changes if the setup touches an application file.

## Inspect the available rails

Read the repository instructions and inspect its working tree. Identify its
languages, package boundaries, existing tool configuration, local validation
commands, CI workflows, release paths, and every `AGENTS.md` and `CLAUDE.md`.
Use this inspection only to choose the smallest native setup. Avoid a broad
quality audit.

Reuse existing tools and entry points. Keep valuable correctness, security,
release, and operational checks in place.

## Add the repository contract

Resolve agent instructions one directory at a time before adding quality
rules. `AGENTS.md` is the canonical record for each directory.

- When sibling `AGENTS.md` and `CLAUDE.md` files both contain instructions,
  merge every unique directive into `AGENTS.md`. Place each directive in the
  section where it fits and remove duplicated wording.
- When a directory has `CLAUDE.md` without `AGENTS.md`, create `AGENTS.md` from
  those instructions.
- When `CLAUDE.md` is a symlink to another target, inspect the resolved content
  and preserve any unique directive in the sibling `AGENTS.md` before changing
  the link.
- After convergence, replace the sibling `CLAUDE.md` with a relative symlink
  whose target is `AGENTS.md`.
- Ensure every `AGENTS.md` in the repository has that sibling symlink. Keep
  nested instructions in their existing directory scope.

Add a concise code-quality section to the root `AGENTS.md`, creating the file
when the repository has no agent instructions. Include the shared goals that
apply to the repository and any project-specific thresholds or commands
established by setup.

The section must tell future agents to:

- keep code and process tied to current product, correctness, security, or
  operational needs;
- favor fast feedback, low ceremony, DRY ownership, composition, and explicit
  dependencies;
- keep authored files and modules within the repository's defined limits;
- write tests around behavior, contracts, state transitions, and failure
  modes;
- reserve exact string assertions for cases where text is the contract;
- preserve `AGENTS.md` as the canonical record and the sibling `CLAUDE.md`
  symlink convention;
- run the canonical quality command before delivery.

Keep the section short enough that future agents will read it. Put detailed
project-specific mechanics in existing tool configuration or one dedicated
quality document when the detail cannot fit cleanly in `AGENTS.md`.

## Build the enforcement rails

Use stack-native mechanisms for standards with reliable mechanical signals.
Common candidates are formatting, linting, type checking, authored source
size, generated-file consistency, dependency boundaries, tests, and builds.

Give the repository one canonical quality command. Make local use, CI, and
release validation call that command when the existing project state supports
required enforcement. Preserve one implementation of each check.

When a newly configured check reports existing application findings, leave the
checker and its command in place for later project work. Keep currently green
required workflows green until the project adopts that check. Do not add
suppressions, allowlists, exception ledgers, or source edits to make the check
pass.

Add the minimum files required by the current stack. Avoid a generic quality
framework, a new package, or a new task runner when existing project tools can
express the rule.

## Verify the rails

Validate new documentation, configuration syntax, scripts, and workflow
references. Confirm that each `CLAUDE.md` resolves to its sibling `AGENTS.md`
and that the canonical file contains the merged instructions. Run newly
configured checks only to confirm their behavior and report their status.
Leave every finding unchanged.

Review the final diff and confirm that it contains only documentation and
quality infrastructure. A second setup run should produce no further changes.

Report the rules added, the enforcement entry points created, and any check
whose adoption remains for later project work.
