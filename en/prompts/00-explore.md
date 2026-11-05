# Task: explore the project before you add documentation

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Goal: understand what the project is and which tools it already has.
Result: the files `docs/_setup/inventory.md` and `docs/_setup/progress.md`.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Create only the files `docs/_setup/inventory.md` and `docs/_setup/progress.md`.
4. Do not change the program code or the specifications.
5. Do not invent names of classes, methods, files, or fields.
   Copy each name from a file that you opened in this session.
6. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
7. Do not make commits or create branches unless the user asks.
8. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**If the work was interrupted:** open `docs/_setup/inventory.md`. Continue from the first section that is not filled in.

## Step 0. Choose the documentation root

The documentation root is the folder that holds all documentation files. By default, it is `docs/`.

1. Check the project root. Find folders with `.md` files, for example `docs/`, `documentation/`, `wiki/`.
2. If there is no `docs/` folder but another documentation folder exists, stop. Ask the user: "The project documentation is in `<folder>/`. Create the documentation files in it or in a new `docs/` folder?"
3. Write down the answer. This is the documentation root.
4. If the documentation root is not `docs/`, replace `docs/` with the documentation root in all paths of this prompt. Example: `docs/_setup/inventory.md` becomes `documentation/_setup/inventory.md`.

In all other cases, the documentation root is `docs/`.

## Step 1. Find files and write down what you found

Check each item. For each item, write "found" (path) or "not found".

**Build and language:**
- `build.gradle`, `build.gradle.kts`, `settings.gradle*`, `pom.xml`, `package.json`, others.
- Project modules (from `settings.gradle` or `pom.xml`).

**Specifications (SDD):**
- `openspec/` — OpenSpec. Write down: `openspec/specs/*`, `openspec/changes/*`, `openspec/config.yaml`.
- `.specify/` or `specs/` — Spec Kit or another tool.
- Other folders with specifications or requirements.

**Instructions for agents:**
- `AGENTS.md`, `CLAUDE.md`, `GIGACODE.md` (in the root and in subfolders).
- `.claude/skills/*/SKILL.md`, `.claude/commands/*`, `.claude/agents/*`.
- `.gigacode/skills/*/SKILL.md`, `.gigacode/commands/*`.
- `.opencode/skills/*/SKILL.md`, `.agents/skills/*/SKILL.md`.
- `.cursor/rules/*`, `.github/copilot-instructions.md`, other files with rules for AI.
- Rules and skills outside the repository. Sign: an instruction file refers to a path outside the project, for example `~/.config/<tool>/AGENTS.md` or `~/.claude/skills/`. Write down the path. Do not open the file. Add a question for the user: whether to take this file into account.

**Documentation:**
- `README.md`, `docs/`, `wiki/`, `adr/`, other folders with `.md` files.
- Glossaries and lists of terms. Look for separate files and for sections inside documents. For example, the "Terms" section in `README.md`. Write down the path and the section name.

**Documentation language:**
- The language of the project specifications and documentation.

**Domain (search):**
- Main packages with business logic (for example, `domain`, `service`, `model`).
- SQL scripts, data schemas.

## Step 2. Read the skills, rules, and documents that you found

For each skill and rules file, write one line:
`<path> — <what it does> — <when it runs>`.

Mark the skills that relate to: review, tasks, specifications, documentation.

For each document from the "Documentation" item of step 1, choose an assessment:
- "current" — the facts from the document match the code;
- "partly outdated" — some facts do not match the code;
- "outdated" — the document describes behavior or a process that no longer exists;
- "unknown" — you could not check the facts.

To choose the assessment, check 2–3 facts from the document against the code: class names, settings, dependencies. Write down the reason: which fact matched or did not match.

## Step 3. Define the areas (capabilities)

- If `openspec/specs/<name>/` exists, each folder = one area.
- If the project has another SDD tool, use its division.
- If the project has no SDD tool, add a question for the user: "The library is for projects with SDD. No SDD tool was found in the project. Continue?" Propose areas by modules or packages of business logic.
- If the specifications are divided by work stages, not by areas, do not use their division. Propose areas by the code. Add a question for the user.

Write down the list of areas. For each area: name, path to the specification (if any), paths to the code.

Paths to the code:
- If the area has its own folder or package, write down the path to it.
- If the code is divided by layers (for example, `controller`, `service`, `repository`), all areas have the same packages. Then for each layer, write down the files of the area or a name mask. Example for the library service: `service/Loan*`, `repository/LoanRepository.java`.
- Each path belongs to only one area. If two areas need one file, add a question for the user.

## Step 4. Write the report

Create `docs/_setup/inventory.md`. Structure:

```markdown
# Project inventory

## Build
<language, build system, modules>

## Specifications
<tool, paths, number of areas>

## Agent skills and rules
| Path | What it does | When it runs | Related to documentation? |
|---|---|---|---|

## Documentation language
<language of the specifications and documentation>

## Existing documentation
| Path | Assessment | Reason |
|---|---|---|

## Areas
| Area | Specification | Paths to the code |
|---|---|---|

## Questions for the user
<list or "none">
```

If the project language does not match the language of this prompt, add a question: which language to use for the documentation. For Russian, use the `ru/` folder of the library. For English, use `en/`.

Create `docs/_setup/progress.md`:

```markdown
# Adoption progress

Documentation root: `<folder>/`

- [x] 00. Explore the project
- [ ] 01. Map
- [ ] 02. Glossary
- [ ] 03. Area guides
- [ ] 04. Integration into the process

## Areas
| Area | analyst.md | dev.md | Verified |
|---|---|---|---|
```

**STOP.** Show `inventory.md` to the user. Ask the questions from the "Questions for the user" section. Wait for an answer.
