# Example papercuts report

This is the target shape and tone: a ranked table, scannable in under a
minute. One row per papercut, worst-recurrence first. Keep cells to one or
two short sentences — a table row that wraps into a paragraph defeats the
format. Exact file paths go in the table; anything genuinely too long for a
cell goes in a short note below the table, not inside it.

---

Two papercuts this session, ranked by priority:

| #   | Papercut                                                                                                                                    | Cost                                                           | Fix                                                                                              |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| 1   | `pnpm test` in `packages/api/` silently runs zero tests — the script targets `tests/` but tests live in `src/**/*.test.ts`, and it exits 0. | Believed my first attempt passed; failure only surfaced in CI. | Point the `test` script at `src/` in `packages/api/package.json`; delete the empty `tests/` dir. |
| 2   | Two copies of the rate-limit config; README names `config/rate-limits.json` but the server reads inline values in `src/server/limits.ts`.   | ~20 min confirming my edit "did nothing".                      | Delete `config/rate-limits.json`; fix the README reference.                                      |

Nothing else meaningfully slowed the work down.

---

Anti-patterns to avoid:

- Ten-row tables where three rows are real. Padding buries the signal.
- Paragraph-length cells. If a cell needs that much text, tighten it or move
  the detail to a note under the table.
- Vague fixes ("improve the docs"). Name the exact file and the exact change.
- Reporting the task's inherent difficulty as friction.
