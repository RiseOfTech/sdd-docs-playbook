# sdd-docs-playbook

A recipe library for readable, up-to-date documentation in projects with SDD (spec-driven development).

You do not install the library. You copy templates, prompts, and skills from it into your project.

> Version 0.1. The rules, templates, prompts, patches, the update and verification skills, and the integration with OpenSpec and with agent instruction files are ready. For changes between versions, see `CHANGELOG.md`.

## Who it is for

For analysts, developers, and team leads.
A ready integration exists for OpenSpec. For another SDD tool, `en/prompts/04-integrate.md` describes how to connect it.

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

## Preparation

The agent copies files from the library into your project. So the agent needs access to the library folder.

1. Download the library. Put it next to your project:

   ```
   ~/dev/
   ├── my-project/          your project
   └── sdd-docs-playbook/   this library
   ```

   To download with git, run this command in the `~/dev/` folder:

   ```
   git clone https://github.com/RiseOfTech/sdd-docs-playbook.git
   ```

   Without git: on the repository page, click "Code", then "Download ZIP". Unpack the archive into `~/dev/sdd-docs-playbook/`.
2. Open the agent in the folder of your project. Do not open the agent in the library folder.
3. Give the agent access to the library folder:
   - Claude Code: run the command `/add-dir ../sdd-docs-playbook`. Another way: start the agent with the command `claude --add-dir ../sdd-docs-playbook`.
   - GigaCode, OpenCode, and other tools: add the library folder to the workspace. To learn how, see the documentation of the tool.
4. Check the access. Write to the agent:

   ```
   Open the file ../sdd-docs-playbook/en/README.md and name its first heading.
   ```

   If the agent cannot open the file, do step 3 again.

## How to run the prompts

1. For each prompt, start a new agent session. Then the work of one prompt fits into one session.
2. Write to the agent:

   ```
   Follow the instructions from the file ../sdd-docs-playbook/en/prompts/00-explore.md
   ```

3. At each **STOP** step, the agent waits for your answer. Check the result and answer.
4. Run the prompts in order:

   | Prompt | How many times | Result |
   |---|---|---|
   | `00-explore.md` | Once | List of project tools, skills, and areas |
   | `01-map.md` | Once | `docs/DOCS-RULES.md`, `docs/MAP.md` |
   | `02-glossary.md` | Once | `docs/glossary.md` and term conflicts |
   | `03-guide-area.md` | For each area | Guides of the area, and `docs/ONBOARDING.md` on the first area |
   | `04-integrate.md` | Once | Patches in the project skills, the `docs-sync` and `docs-review` skills |
   | `05-audit.md` | Once a month or a quarter | Report on outdated guides |

   The agent marks finished stages in `docs/_setup/progress.md`.

For a small project, use one prompt: `en/prompts/full-setup.md`.

## How to start without an agent

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

## What is in the repository

| Path | What it is |
|---|---|
| `en/templates/docs/` | Templates: rules, map, route, glossary, guides |
| `en/prompts/` | One-time tasks for an agent |
| `en/patches/` | Inserts for project skills. Start with `en/patches/README.md` |
| `en/skills/` | The `docs-sync` (update) and `docs-review` (verification) skills |
| `en/integrations/` | Setup for OpenSpec and for agent instruction files |

## Plans

- A skill to add and rename terms.
- A skill that answers questions about the project from the map and the guides.
- Explanation of the idea for people. Notes on large projects and weaker models.
- An open example project with documentation built by this library.

## License

MIT. See `LICENSE`.
