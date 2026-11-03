# spec

Read the published [Standard Agent Specification](https://standardagentspec.org)
when a question or a piece of work depends on it. The skill applies to any
conforming runtime.

```bash
npx skills add standardagents/skills@spec
```

## Usage

Invoke `/spec` with a question, or let your coding agent load the skill when it
works on anything that must conform to the specification.

## Version updates

The skill holds no specification content. It reads `llms.txt` and the page URLs
it lists each time it runs, so a new specification version reaches installed
copies when the site deploys that version.

Run `npx skills update` only to get changes to the skill's reading instructions.

Keep these published endpoints stable, or update the skill in the same change:

- `/llms.txt` and its `Latest version:` line
- `/api/navigation/<version>.json`
- `/<version>/<group>/<page>.md`
