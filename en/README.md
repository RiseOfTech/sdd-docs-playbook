# sdd-docs-playbook

A recipe library for readable, up-to-date documentation in projects with SDD (spec-driven development).

You do not install the library. You copy templates, prompts, and skills from it into your project.

> Status: draft. The rules, templates, prompts, patches, and the update and verification skills are ready. See the table "What is in the repository".

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

## How it works

1. Once: create the documentation: the map, the glossary, the rules, the first guides.
2. Once: connect the skills: copy `docs-sync` and `docs-review`, insert the patches into the project skills.
3. Then work as usual.
4. After you implement a change, `docs-sync` updates the guides, the glossary, and the map.
5. Before a review and an archive, `docs-review` checks the documentation.
6. If `docs-review` finds errors, the `archive.md` patch forbids the archive.

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
| `en/templates/docs/` | Templates: rules, map, route, glossary, guides | Ready |
| `en/prompts/` | One-time tasks for an agent | Ready |
| `en/patches/` | Inserts for project skills. Start with `en/patches/README.md` | Ready |
| `en/skills/docs-sync/`, `en/skills/docs-review/` | Update and verification skills | Ready |
| `en/integrations/openspec.md`, `en/integrations/agents-md.md` | Setup for OpenSpec and agent instruction files | Ready |
| Other files in `en/skills/` and `en/integrations/` | Other skills and integrations | In progress |
| `en/concepts/` | Explanation of the idea for people | In progress |
| `en/notes/` | Large projects, weaker models | In progress |

## License

MIT. See `LICENSE`.
