# sdd-docs-playbook

A recipe library for readable, up-to-date documentation in projects with SDD (spec-driven development).

You do not install the library. You copy templates, prompts, and skills from it into your project.

> Status: draft. The rules, templates, and prompts are ready. See the table "What is in the repository".

## Who it is for

For analysts, developers, and team leads. It fits projects with OpenSpec, Spec Kit, or without SDD.

## What problem it solves

A new person opens the project map. The map shows which guides to read.
The rules are in one file. Skills and agent instructions only refer to it.

## What the project gets

```
docs/
├── MAP.md            project map: the entry point for a new person
├── ONBOARDING.md     reading route by role
├── DOCS-RULES.md     single set of rules
├── glossary.md       glossary: one term = one meaning
└── guide/
    ├── _template/    guide templates
    └── <area>/
        ├── analyst.md   what and why
        └── dev.md       how and where
```

## Quick start

1. Create the `docs/` folder in your project.
2. Copy `en/templates/docs/DOCS-RULES.md` to `docs/DOCS-RULES.md`.
3. Copy `en/templates/docs/MAP.md` to `docs/MAP.md`.
4. Copy `en/templates/docs/glossary.md` to `docs/glossary.md`.
5. Fill in the map. The instructions are at the start of the file.
6. Add this section to `AGENTS.md`, `CLAUDE.md`, or `GIGACODE.md`:

   ```markdown
   ## Documentation
   - Rules: `docs/DOCS-RULES.md`. Glossary: `docs/glossary.md`.
   - After a change to a specification or to code behavior, update the guides by `docs/DOCS-RULES.md`, section 6 "How to update".
   - For domain concepts, use only terms from the glossary.
   ```
7. If the project has skills, connect them by `en/patches/README.md`.

To let an AI agent do this work, run the prompts from `en/prompts/` in order: from `00-explore.md` to `04-integrate.md`.
For a small project, use one prompt: `en/prompts/full-setup.md`.

## What is in the repository

| Path | What it is | Status |
|---|---|---|
| `en/templates/docs/DOCS-RULES.md` | Single set of rules: writing, glossary, updates, verification, report | Ready |
| `en/templates/docs/MAP.md` | Project map template | Ready |
| `en/templates/docs/` | Other templates: route, glossary, guides | Ready |
| `en/prompts/` | One-time tasks for an agent | Ready |
| `en/patches/README.md` | How to find the skill type and what to insert into it | Ready |
| `en/patches/` | Patch files | In progress |
| `en/skills/` | New skills to copy | In progress |
| `en/integrations/` | Setup for a specific tool | In progress |
| `en/concepts/` | Explanation of the idea for people | In progress |
| `en/notes/` | Large projects, weaker models | In progress |

## License

MIT. See `LICENSE`.
