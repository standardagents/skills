# Shared code-quality standards

These standards define the quality contract. A repository's stack determines
the enforcement mechanism.

## Current value

Every production component, abstraction, workflow, recurring process, and
quality check needs a clear connection to current product behavior,
correctness, security, durability, compatibility, operations, or recovery.

Avoid process porn: ceremony whose detail exceeds its decision or safety
value. Use the shortest workflow that protects the named requirement.

Avoid self-licking ice cream code: machinery whose primary consumer is more of
the same machinery. Internal frameworks, adapters, registries, generators, and
metadata layers need a current external outcome.

## Fast feedback

Use one canonical quality command. Put fast deterministic checks before slower
integration checks, including a zero-compiler (<1s) structural check on
pre-push. Match validation depth to behavior and risk, and exclude pure
agent-instruction edits (`AGENTS.md` and `CLAUDE.md` at any depth) from
build-and-test change-detection filters. Keep routine commands non-interactive.
Preserve expensive checks that cover a named failure domain.

## DRY ownership

Keep each fact, rule, and behavior in one authoritative place when its copies
must change together. Consolidate duplicated logic that represents the same
invariant. Extract an abstraction after shared responsibility and ownership are
clear.

## Composition and explicit dependencies

Favor small components with explicit inputs, outputs, ownership, and failure
behavior. Use composition, delegation, and data flow where the language offers
them. Keep side effects at visible boundaries.

## File cohesion, layout, and source size

Keep each authored file or module focused on one coherent concern. Code for a
different concern belongs in an existing module that owns that concern or in a
new module with a clear responsibility that can accommodate related growth.
Utilities and other supporting concerns should be imported through explicit
interfaces. Code that changes together should remain together.

Separate non-test source size from test files and inline test blocks so thorough
tests never force artificial splits. As a general baseline when the repository
has no more suitable threshold, target about 1,800 non-test lines for newly
authored non-test files and about 3,000 physical lines as an upper ceiling.
Crossing the baseline prompts a cohesion review. Shorter files also warrant
review when they combine unrelated behavior, while a cohesive file may justify
a larger size. Any extraction should establish meaningful ownership for the
resulting modules.

Keep source layout predictable for both humans and agents:

- group files into semantic domain subdirectories (`src/<domain>/`) once a flat
  source directory grows past roughly 25 direct source files;
- keep the filesystem layout aligned with the language's module graph rather
  than hiding file locations behind path overrides, barrel-file mazes, or
  import-path aliases;
- avoid grab-bag filenames (`helpers`, `utils`, `common`, `misc`, `extra`);
- start new non-test source files with a 1-line ownership header (module
  docstring or leading comment) so readers can scan a directory's ownership
  without opening every file.

Define mechanical limits for authored files, modules, functions, and source
line width only where they produce a stable, low-noise signal. Exclude generated
and vendored code explicitly. Repository conventions and language ecosystems
may justify different thresholds.

## Tests with behavioral value

A useful test fails when a supported behavior, invariant, boundary, or failure
mode breaks. It should survive internal refactoring that preserves the
contract.

Exact text assertions serve protocols, parsers, serializers, generated files,
command output, and user-visible copy when text is the contract. Source-text
matching, private implementation-name assertions, and tests that repeat a
constant from the same change provide little protection.

Use integration and end-to-end tests for boundaries that unit tests cannot
represent faithfully. Avoid mocks that duplicate the implementation under
test.

## Agent documentation

Use `AGENTS.md` as the canonical instruction file. Every `AGENTS.md` has a
sibling `CLAUDE.md` symlink whose relative target is `AGENTS.md`. Merge unique
content from an existing `CLAUDE.md` into its sibling `AGENTS.md` before
replacing the file or changing its link. A directory with only `CLAUDE.md`
receives an `AGENTS.md` containing those instructions before the symlink is
created. Enforce symlink integrity in the fast pre-push check.

Keep root `AGENTS.md` short (around 200 lines or fewer) so it stays cheap to
read on every task. Root instructions hold shared standards and trigger-indexed
pointers to deeper reference docs. Add nested `AGENTS.md` files only where a
high-churn subtree or distinct runtime boundary has meaningful local
differences.

Documentation should state decisions, invariants, commands, ownership, and
failure recovery. Keep implementation inventories on the surfaces that own
them.

## Enforcement

Mechanically enforce standards that produce stable, low-noise signals. Keep
design judgment in agent instructions and code review guidance. Reuse the
repository's existing formatter, linter, type checker, package scripts, build
system, and CI provider.

Prefer diff-scoped ratchets over unwired checks or exception ledgers: apply
strict limits to new files, cap per-branch growth on existing oversized files,
and expose a non-blocking audit mode to guide planned cleanup waves.

Quality setup creates the rule and its enforcement path. Later project work
resolves findings and improves application code.
