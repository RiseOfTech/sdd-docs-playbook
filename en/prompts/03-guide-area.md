# Task: write the guides of one area

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Run this prompt separately for each area.

Goal: explain one area for the analyst and the developer.
Result: the files `docs/guide/<area>/analyst.md` and `docs/guide/<area>/dev.md`, and links to them in `docs/MAP.md`.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Change only the folder `docs/guide/`, the files `docs/glossary.md`, `docs/MAP.md`, `docs/ONBOARDING.md`, and the folder `docs/_setup/`.
   Change `docs/DOCS-RULES.md` only if the user asks at step 10.
4. Do not change the program code or the specifications.
5. Do not invent names of classes, methods, files, or fields.
   Copy each name from a file that you opened in this session.
6. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
7. Work on one area at a time. Finish the area, then start the next one.
8. Do not make commits or create branches unless the user asks.
9. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**If the work was interrupted:** open `docs/_setup/facts-<area>.md` and the guides of the area. Continue from the first step that is not finished.

## Step 1. Read the result of the previous stages

1. Open `docs/DOCS-RULES.md`. Read the whole file.
2. Open `docs/glossary.md`.
3. Open `docs/MAP.md`.
4. Open `docs/_setup/progress.md`.

If one of the files does not exist, stop. Tell the user: "Run the prompt `02-glossary.md` first."

## Step 2. Choose the area

- If the user named an area, use it.
- Otherwise, take the first area in the "Areas" table of `progress.md` that has no guides.

If this is the first area, choose it with the user: medium size, has a specification, clear code.

## Step 3. Copy the templates

If the folder `docs/guide/_template/` does not exist, copy the files from the `sdd-docs-playbook` library:

| From | To |
|---|---|
| `en/templates/docs/guide/_template/analyst.md` | `docs/guide/_template/analyst.md` |
| `en/templates/docs/guide/_template/dev.md` | `docs/guide/_template/dev.md` |

Paths `en/...` start from the library folder. Usually it is next to the project: `../sdd-docs-playbook/`.
If you have no access to the library files, stop. Ask the user to give access by the library file `en/README.md`, section "Preparation". Do not write the text of library files from memory.

## Step 4. Collect the facts

1. Read the whole specification of the area, if it exists.
2. Find the entry point: a controller, a scheduled task, a message listener, a public method.
3. Follow the code from the entry point. Write down the call chain: `Class.method()` → `Class.method()`.
4. Write down all conditions (`if`, `switch`, exceptions) that change the result.

Write the facts to `docs/_setup/facts-<area>.md`. This is a draft. The user does not read it.

## Step 5. Write `analyst.md`

If the area is in the "Service areas" section of `docs/MAP.md`, skip this step.

1. Copy `docs/guide/_template/analyst.md` to `docs/guide/<area>/analyst.md`.
2. Follow the instructions at the top of the file.

## Step 6. Write `dev.md`

1. Copy `docs/guide/_template/dev.md` to `docs/guide/<area>/dev.md`.
2. Follow the instructions at the top of the file.

## Step 7. Add new terms

If you found a new term, add it to `docs/glossary.md`. Write down the term for the report.

## Step 8. Verify the guides

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Fix all "no" items.

If a guide is longer than 60 lines, propose to the user to split the area. Do not split it yourself.

## Step 9. Update the map and the route

1. In `docs/MAP.md`, replace "none" in the "Guides" column with links to the guides of the area.
2. If the file `docs/ONBOARDING.md` does not exist, copy `en/templates/docs/ONBOARDING.md` to `docs/ONBOARDING.md`. Follow the instructions at the top of the file.
3. If the file `docs/ONBOARDING.md` already existed and the area is important for a person who does not know the project, add rows for the area to the role tables.
4. Update the "Areas" table in `docs/_setup/progress.md`.
5. If all areas have guides, mark stage 03 in `progress.md`.
6. If stage 04 is already marked in `progress.md`, delete `docs/_setup/facts-<area>.md`.

## Step 10. Show the result

Print the report by `docs/DOCS-RULES.md`, section 8 "Report after the update".

**STOP.** If this is the first area, show both guides and the verification result. Ask:
1. Is `analyst.md` clear to an analyst?
2. Is `dev.md` enough for a developer to find the place to change?
3. What should change in the templates or rules?

If the user asks to change the templates or rules, change `docs/DOCS-RULES.md` and the templates. Then redo the guides of this area.

If this is not the first area, show only the report.
