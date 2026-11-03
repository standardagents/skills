---
name: spec
description: Read the published Standard Agent Specification before answering questions about it or before writing, reviewing, or checking anything that must conform to it. Use for Standard Agent models, prompts, tools, hooks, agents, subagents, threads, runtimes, packaging, and portability questions, and when deciding whether behavior is required by the specification or specific to one implementation.
---

# Standard Agent Specification

The published specification is the only source of truth. This skill holds no
specification rules, so read the pages at use time. Do not answer from memory,
and do not rely on a remembered version number.

## 1. Choose the version

Fetch the index:

```text
https://standardagentspec.org/llms.txt
```

Its `Latest version:` line names the latest version. The index lists a raw
markdown URL for every page of that version.

Use the latest version unless the user or the project names another version.
Check the project's documentation and its implementation's documentation for a
named version. If you find none, use the latest version and say so.

For a named older version, fetch its navigation:

```text
https://standardagentspec.org/api/navigation/<version>.json
```

Each `href` in that file becomes a raw markdown URL when you add
`https://standardagentspec.org` before it and `.md` after it. Archived versions
do not change. Tell the user when a newer version exists.

## 2. Read the relevant pages

Choose pages by their titles in the index. Read every page that governs the
question, because behavior can cross pages. Follow links to related pages when
a page depends on them.

Treat a response as not found unless its content type is `text/markdown`, or
`text/plain` for `llms.txt`. The site can return an HTML page with status 200
for an unknown path. Build URLs only from the index or the navigation file.

The current models guide listed in the index is a practical snapshot. It is not
part of the normative specification.

## 3. Report what the specification says

- Name the version and link the pages you used.
- Separate required behavior from recommendations and from your own inference.
- Say so when the specification does not define something. Do not fill the gap
  with the behavior of a runtime, package, or vendor product.
- Treat an implementation's types, source, and documentation as evidence of
  that implementation only. When one disagrees with the specification, report
  the disagreement.
- Keep advice about portable agents to published specification surfaces.

If you cannot reach the site, tell the user. Label anything you then say from
memory as unverified.
