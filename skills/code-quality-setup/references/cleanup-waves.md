# Cleanup waves after quality setup

`code-quality-setup` lays the rails without editing application code. When
follow-up tasks act on the repository's `--audit` output (splitting oversized
files, grouping flat directories, or removing module-path redirects), use this
checklist to avoid breaking active work.

## Stay zero-overlap with in-flight branches

Before moving or splitting files in a multi-branch or multi-agent repository,
compute the file footprint of every active long-lived branch against its merge
base with the default branch and exclude overlapping files (`comm -12`).

- Do not move or split files actively modified on long-lived feature branches.
- Do not relocate child files that are loaded through a relative path override
  from an untouched parent file on an active branch; wait until the parent can
  move too.
- Skip frozen security, cryptography, or release-baseline paths unless
  explicitly authorized for review.

## Keep waves small and bisectable

- Group changes into focused, reviewable waves by concern (directory grouping,
  oversized-file splits, path-redirect removal, dead-code pruning).
- Ensure every commit in a multi-commit wave builds and passes syntax checks
  standalone.
- Treat pure internal refactors as internal changes with no user-facing
  changelog noise.

## Audit file-move side effects

Moving or splitting files without changing public behavior can still break
path- or target-sensitive contracts. Check each of these before running full
gates:

- **Relative asset and fixture paths:** Update relative includes, fixtures,
  templates, or snapshot paths when a file changes directory depth.
- **Exact test and harness filters:** Search scripts, CI workflows, and
  subprocess tests for hardcoded module paths or exact test-name filters.
- **Cross-target and platform guards:** Preserve conditional compilation,
  build-tag, or platform-specific import guards across every supported target
  and OS, not only the local development host.
- **Public API and visibility boundaries:** Re-export moved public items at
  their existing boundary and keep new internal helpers narrowly scoped.

## Verify each wave

Run the fast structural hygiene check (`branch`, `--full`, and `--audit`
before/after), confirm zero overlap against open branches, and pass the
repository's canonical quality command before integrating.
