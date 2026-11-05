# Integration with agent instruction files

Use this file if the project has an instruction file for an AI agent.

Goal: the agent knows the documentation rules in each session.
Do not copy the rules. Give only a link to `docs/DOCS-RULES.md`.

## Step 1. Find the instruction files

Check the project root. For each file, write down: exists or does not exist.

| Tool | File |
|---|---|
| Different agents | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |
| GigaCode | `GIGACODE.md` |

GigaCode reads only `GIGACODE.md`. It does not read `AGENTS.md` and `CLAUDE.md`.
If the team works in GigaCode, the section must be in `GIGACODE.md`.

If no file exists, ask the user which tool the team uses. Do not create a file yourself.

## Step 2. Add the section

Add this text to the end of each file that you found. Do not change the rest of the file.

```markdown
## Documentation
- Rules: `docs/DOCS-RULES.md`. Glossary: `docs/glossary.md`.
- After a change to a specification or to code behavior, update the guides by `docs/DOCS-RULES.md`, section 6 "How to update".
- For domain concepts, use only terms from the glossary.
```

## How to merge with existing text

1. If the file already has a "Documentation" section, do not create a second one. Add the lines to the end of that section.
2. If the file has a section with the same purpose under a different name, ask the user: add the lines to that section or create a "Documentation" section. Example: a "References" section with links to project documents.
3. If a line contradicts the existing text, do not change the existing text. Ask the user.
4. If one file only links to another, add the section to the file it links to. Exception: `GIGACODE.md`. Add the section to `GIGACODE.md` itself.
