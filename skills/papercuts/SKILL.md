---
name: papercuts
description: Retrospective on codebase friction. Use when the user invokes /papercuts, usually after a task, to report what about the codebase made the job harder than it needed to be — confusing structure, stale docs, misleading names, missing tooling — so recurring friction can be identified and fixed.
---

# Papercuts

The user wants to know what slowed you down. Not the task itself — the
friction around it: things about the codebase, docs, or tooling that made the
job harder than it needed to be, sent you down a wrong path, or forced you to
figure out something that should have been written down.

This is a retrospective, **not** a request to fix anything. Report findings
only; do not edit files unless the user explicitly asks afterward.

## What to review

Walk back through the work you did this session and ask, for each stumble or
detour:

- **Wrong paths taken.** Did you start editing the wrong file, wrong package,
  or wrong layer? What signal misled you (a stale doc, a duplicate copy, a
  misleading name)?
- **Discovery cost.** What took multiple searches or file reads to find that a
  README, index, or better name would have made instant? What did you have to
  infer from code that should be documented?
- **Docs vs reality.** Where did CLAUDE.md/AGENTS.md/README/comments say
  something the code contradicted? Stale docs are worse than no docs — call
  them out specifically.
- **Duplication and drift.** Did the same logic, config, or docs exist in
  multiple places? Which copy is canonical, and was that discoverable?
- **Tooling friction.** Commands that failed on first try, missing scripts,
  setup steps that weren't documented, tests that couldn't be run in isolation,
  slow or flaky feedback loops.
- **Structural confusion.** Naming that doesn't match behavior, files in
  surprising locations, god-files, unclear ownership boundaries between
  packages/repos.
- **Traps you nearly fell into.** Anything where you were saved only by luck
  or an existing memory/note — the next agent won't be.

## What NOT to report

- **Anything already fixed.** If the friction was resolved during the session
  (by you or the user), it is not a papercut — the table is a to-do list of
  open, actionable items only. At most, note fixed items in one summary line
  below the table ("also hit and fixed: X, Y"); never give them a row.
- The inherent difficulty of the task itself.
- Style preferences with no confusion cost ("I'd have used X library").
- Friction from your own tooling or the harness, unless the repo could
  reasonably absorb it (e.g. a missing npm script).
- Speculative issues in code you never touched.

## Proactive suggestion

At the end of any task where the codebase itself caused real trouble — any of
the friction categories above: a wrong path taken, stale or contradictory
docs, a misleading duplicate, tooling that failed or lied, structure that
took repeated searching to decode — append one line to your final summary:
"This session hit codebase friction; run `/papercuts` for a breakdown."
Suggest it only when friction actually cost you time; do not offer it after
smooth sessions.

## Output format

Match the shape in [references/example.md](references/example.md): a ranked
table with one row per papercut (Papercut / Cost / Fix), worst-recurrence
first, cells kept to one or two short sentences. Scannable in under a minute
— no prose padding.

For each papercut (aim for the real handful, not a padded list):

1. **What happened** — the concrete moment of friction, with file paths.
2. **Cost** — what it caused: wrong path for N minutes, repeated searching,
   an incorrect first attempt, etc.
3. **Suggested fix** — the smallest durable change that prevents a repeat:
   a doc line, a rename, a deleted duplicate, an added script. Name the exact
   file the fix belongs in.

Rank by expected recurrence: the papercut every future agent will hit goes
first. Every row must be open and actionable — something the user could fix
right now. If nothing meaningfully slowed you down, say so plainly — a forced
list of trivia dilutes the signal.
