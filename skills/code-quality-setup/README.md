# code-quality-setup

Set up repository code-quality rules and stack-appropriate enforcement rails
without changing application code.

```bash
npx skills add standardagents/skills@code-quality-setup
```

## Usage

Invoke `/code-quality-setup` in the repository you want configured. The skill
converges agent instructions into canonical `AGENTS.md` files with sibling
`CLAUDE.md` symlinks. It also adds native quality configuration, a canonical
check path, and CI or release wiring appropriate to the current stack.

Application cleanup, refactoring, tests, and quality findings remain project
work after setup.
