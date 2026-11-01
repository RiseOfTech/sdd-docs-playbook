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
- `.gigacode/skills/*/SKILL.md`, `.opencode/skills/*/SKILL.md`, `.agents/skills/*/SKILL.md`.
- `.cursor/rules/*`, `.github/copilot-instructions.md`, other files with rules for AI.

**Documentation:**
- `README.md`, `docs/`, `wiki/`, `adr/`, other folders with `.md` files.

**Domain (search):**
- Main packages with business logic (for example, `domain`, `service`, `model`).
- SQL scripts, data schemas.

## Step 2. Read the skills and rules that you found

For each skill and rules file, write one line:
`<path> — <what it does> — <when it runs>`.

Mark the skills that relate to: review, tasks, specifications, documentation.

## Step 3. Define the areas (capabilities)

- If `openspec/specs/<name>/` exists, each folder = one area.
- If the project has another SDD tool, use its division.
- If there are no specifications, an area = a module or a main package of business logic.

Write down the list of areas. For each area: name, path to the specification (if any), main code package.

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

## Existing documentation
<paths and a short assessment: current / outdated / unknown>

## Areas
| Area | Specification | Main package |
|---|---|---|

## Questions for the user
<list or "none">
```

Create `docs/_setup/progress.md`:

```markdown
# Adoption progress

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
