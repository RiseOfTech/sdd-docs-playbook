# Task: create the project map

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Goal: show the project areas and the documents for each area.
Result: the files `docs/DOCS-RULES.md` and `docs/MAP.md`. Do not write guides at this stage.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Change only the files `docs/DOCS-RULES.md`, `docs/MAP.md`, and `docs/_setup/progress.md`.
4. Do not change the program code or the specifications.
5. Do not invent names of areas, files, or folders.
   Copy each name from `docs/_setup/inventory.md` or from a folder that you opened in this session.
6. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
7. Do not make commits or create branches unless the user asks.
8. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**If the work was interrupted:** open `docs/MAP.md`. Continue from the first block that is not filled in.

## Step 1. Read the result of the previous stage

1. Open `docs/_setup/inventory.md`.
2. Open `docs/_setup/progress.md`.

If one of the files does not exist, stop. Tell the user: "Run the prompt `00-explore.md` first."

## Step 2. Copy the templates

Copy the files from the `sdd-docs-playbook` library:

| From | To |
|---|---|
| `en/templates/docs/DOCS-RULES.md` | `docs/DOCS-RULES.md` |
| `en/templates/docs/MAP.md` | `docs/MAP.md` |

Paths `en/...` start from the library folder. Usually it is next to the project: `../sdd-docs-playbook/`.
If you have no access to the library files, stop. Ask the user to give access by the library file `en/README.md`, section "Preparation". Do not write the text of library files from memory.
If a file already exists in `docs/`, stop and ask the user.

## Step 3. Fill in the map

Follow the instructions at the top of `docs/MAP.md`. Apply these conditions:

- Keep the `docs/ONBOARDING.md` row in the "Where to find the answer" table. The file appears at stage 03.
- In the "Guides" column, write "none". Guides appear at stage 03.
- If the owner of an area is unknown, write `[VERIFY: area owner]`.
- If there are no service areas, delete the "Service areas" section.
- Fill in the "Other documents" section from the "Existing documentation" section of `inventory.md`. If there are no documents, delete the section.

## Step 4. Verify the map

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Use only the "Map (`docs/MAP.md`)" block. Fix all "no" items.

## Step 5. Update the progress

1. Mark stage 01 in `docs/_setup/progress.md`.
2. Add each area to the "Areas" table.

**STOP.** Show `docs/MAP.md` to the user. Show all `[VERIFY]` marks in a separate list. Ask:
1. Are the block names clear?
2. Is the reading order correct?
3. Who owns the areas without an owner?

Wait for an answer. After the answer, fix the map.
