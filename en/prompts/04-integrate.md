# Task: integrate the documentation into the process

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Goal: make sure that guides are updated with each change.
Result: the file `docs/_setup/plan.md`, changed skills and configs, and the final report.

Run this prompt after the pilot guides. You can write the guides of other areas later.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Change only the files from `docs/_setup/plan.md` and `docs/_setup/progress.md`.
4. Do not change the program code or the specifications.
5. Do not copy the text of the rules into skills and configs. Give only a link to `docs/DOCS-RULES.md`.
6. Do not replace or delete project skills. You can only propose a replacement in the plan.
7. If two skills contradict each other, write the contradiction in the plan. Do not fix it yourself.
8. Do not invent names of files or skills. Copy each name from a file that you opened in this session.
9. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
10. Do not make commits or create branches unless the user asks.
11. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**If the work was interrupted:** open `docs/_setup/plan.md`. Continue from the first item that is not done.

## Step 1. Read the result of the previous stages

1. Open `docs/_setup/inventory.md`. Find the "Agent skills and rules" section.
2. Open `docs/DOCS-RULES.md`.
3. Open `docs/_setup/progress.md`.
4. Open the library file `en/patches/README.md`.

If one of the files in `docs/` does not exist, or `docs/guide/` has no guides, stop. Tell the user: "Run the prompt `03-guide-area.md` first."
If you have no access to the library files, ask the user to add them. Do not write their text from memory.

## Step 2. Decide for each existing skill

For each skill that relates to review, tasks, specifications, or documentation, choose one action:

| Action | When to choose it |
|---|---|
| **Keep** | The skill does not touch documentation. |
| **Add a patch** | The skill matches a type from the table in `en/patches/README.md`. |
| **Propose a replacement** | The skill already creates similar documentation, but of lower quality. |

## Step 3. Decide where to integrate guide updates

Choose all rows of the table that apply.

| If the project has | Integrate like this |
|---|---|
| `openspec/config.yaml` | By the file `en/integrations/openspec.md`. |
| Another SDD tool with a task template | By the file `en/integrations/spec-kit.md`. |
| `AGENTS.md`, `CLAUDE.md`, or `GIGACODE.md` | By the file `en/integrations/agents-md.md`. |
| A skills folder | Copy `en/skills/docs-sync/` and `en/skills/docs-review/` to the skills folder of the project. |
| None of these | By the file `en/integrations/no-sdd.md`. |

## Step 4. Write the plan

Create `docs/_setup/plan.md`:

```markdown
# Integration plan

## Create
- <file> — <why>

## Change
- <file> — <which lines to add> — <why>

## Skills
| Skill | Action | What exactly |
|---|---|---|

## Contradictions and risks
<list or "none">
```

**STOP.** Show the plan. Wait for a confirmation or changes.

## Step 5. Carry out the plan

1. Do the plan items one at a time.
2. For each skill with the "Add a patch" action, open the patch file. Insert its text by the instructions in `en/patches/README.md`.
3. Do not change the rest of the text in skills and configs.
4. Mark the finished items in `docs/_setup/plan.md`.

## Step 6. Update `README.md`

Add this section to the project `README.md`:

```markdown
## Documentation
- Project map: `docs/MAP.md`.
- How the project works for the analyst and the developer: `docs/guide/`.
- Terms: `docs/glossary.md`.
- Maintenance rules: `docs/DOCS-RULES.md`.
```

## Step 7. Do the final check

1. For each area, check that `analyst.md` and `dev.md` exist. Write down areas without guides for the report.
2. Choose 3 random guides. If there are fewer guides, choose all. Follow `docs/DOCS-RULES.md`, section 7 "Verification", for them again.
3. Check that each changed skill and config links to `docs/DOCS-RULES.md` and does not copy the rules.
4. Collect all `[VERIFY]` marks from the guides into one list.
5. Delete the drafts `docs/_setup/facts-*.md`. Keep `inventory.md`, `plan.md`, and `progress.md`.
6. Mark stage 04 in `docs/_setup/progress.md`.

## Step 8. Print the final report

```
Created: <files>
Changed: <files and what was added>
Areas: <N>, guides: <M>
Areas without guides: <list or "none">
Terms in the glossary: <N>
Open questions ([VERIFY] and conflicts): <list>
How to work from now on:
  - after a change: <command or skill>
  - for a review: <command or skill>
```
