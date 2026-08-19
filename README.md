# Standard Agents Skills

Agent skills from the [Standard Agents](https://standardagents.ai) team, for
Claude Code, Codex, and any tool that reads `SKILL.md` packages.

Install any skill with the [skills CLI](https://skills.sh/):

```bash
npx skills add standardagents/skills@<skill>
```

Add `-g` to install user-level instead of per-project. Update later with
`npx skills update`.

## Skills

| Skill | Invoke | Description |
|-------|--------|-------------|
| [bro](skills/bro/) | `/bro` | Snap a verbose agent into concise mode — lead with the answer, technical English, no padding. Rules stay active for the session. |
| [papercuts](skills/papercuts/) | `/papercuts` | Post-task retrospective on codebase friction — what made the job harder than it needed to be, reported as a ranked table of concrete fixes. |
| [streamline](skills/streamline/) | `/streamline` | Reduce unnecessary complexity in technical plans and implementations while preserving current requirements and safeguards. |

Each skill's directory has its own README with usage details.

## Troubleshooting

If Claude Code doesn't see a skill after a global install, the CLI may have
skipped the Claude symlink. Create it manually:

```bash
ln -s ~/.agents/skills/<skill> ~/.claude/skills/<skill>
```

Or reinstall with the agent forced: `npx skills add -g -a claude-code standardagents/skills@<skill>`.
