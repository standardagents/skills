# Standard Agents Skills

Agent skills from the [Standard Agents](https://standardagents.ai) team, for
Claude Code, Codex, and any tool that reads `SKILL.md` packages.

Install with the [skills CLI](https://skills.sh/):

```bash
npx skills add standardagents/skills@papercuts
```

## Skills

| Skill | Description |
|-------|-------------|
| [papercuts](skills/papercuts/SKILL.md) | Post-task retrospective on codebase friction — what made the job harder than it needed to be (stale docs, misleading names, duplicated config, lying tooling), reported as a ranked table of concrete fixes. |

## Usage

Invoke after a work session, typically as `/papercuts`. The skill reports
findings only — it never edits files unless you ask afterward. Output is a
ranked table (Papercut / Cost / Fix) designed to be scannable in under a
minute; see [the example report](skills/papercuts/references/example.md).
