# dmux-rs scope example

This example separates rail laying from application improvement.

## Before

At commit `5c9c124`, dmux-rs had strong rendering-specific validation and few
general quality rails:

- `AGENTS.md` documented the incident loop, issue workflow, validation, and
  release process without a general code-quality contract.
- `CLAUDE.md` was a correct sibling symlink to `AGENTS.md`, so setup preserved
  it without adding another documentation source.
- `crates/dmux/src/main.rs` had 5,291 physical lines.
- `crates/dmux/build.rs` supplied release metadata without a source-size check.
- `scripts/release.sh` ran tests, built binaries, and ran the fidelity harness.
  Formatting and warning-denied Clippy were outside the required path.
- Pull requests and pushes to `main` had no quality workflow.

## Rails added

The repository setup established:

- a concise `Code quality` section in `AGENTS.md`;
- preservation of `AGENTS.md` as the canonical instruction record and the
  existing sibling `CLAUDE.md` symlink;
- an authored-module size checker in the existing Rust build infrastructure;
- one `scripts/check.sh` entry point for formatting, Clippy, and tests;
- a quality workflow that calls the canonical command and preserves fidelity
  validation;
- release wiring that calls the same canonical command.

The broader engineering session also resolved existing formatter and Clippy
findings. Those application edits demonstrate the work this skill must leave
for a separate project task. Source cleanup, tests, and refactoring sit outside
setup scope.

## Expected trajectory

Future agents read the quality contract and use the canonical command. They
keep new modules within the configured limit and address findings as part of
ordinary feature, bug, and refactoring work. A later task can extract cohesive
responsibilities from `main.rs` and strengthen enforcement without changing
the setup skill.
