# papercuts

Post-task retrospective on codebase friction: what made the job harder than
it needed to be — stale docs, misleading names, duplicated config, lying
tooling — so recurring friction gets identified and fixed.

```bash
npx skills add standardagents/skills@papercuts
```

## Usage

Invoke after a work session, typically as `/papercuts`. The skill reports
findings only — it never edits files unless you ask afterward.

Output is a ranked table (Papercut / Cost / Fix), worst-recurrence first,
designed to be scannable in under a minute; see the
[example report](references/example.md). Agents will also proactively suggest
running it at the end of a session where codebase friction cost real time.
