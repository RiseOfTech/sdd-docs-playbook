# Task: build the project glossary

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Goal: collect the project terms.
Result: the file `docs/glossary.md` and a list of conflicts for the user.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Change only the files `docs/glossary.md` and `docs/_setup/progress.md`.
4. Do not change the program code or the specifications.
5. Do not invent names of classes, methods, files, or fields.
   Copy each name from a file that you opened in this session.
6. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
7. Work on one area at a time. Do not keep several areas in progress.
8. Do not make commits or create branches unless the user asks.
9. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**If the work was interrupted:** open `docs/glossary.md`. Continue from the next area in `docs/MAP.md`.

## Step 1. Read the result of the previous stage

1. Open `docs/MAP.md`. Take the list of areas from it.
2. Open `docs/DOCS-RULES.md`. Read section 4 "Glossary".
3. Open `docs/_setup/progress.md`.

If one of the files does not exist, stop. Tell the user: "Run the prompt `01-map.md` first."

## Step 2. Copy the template

Copy the file from the `sdd-docs-playbook` library:

| From | To |
|---|---|
| `en/templates/docs/glossary.md` | `docs/glossary.md` |

Paths `en/...` start from the library folder. Usually it is next to the project: `../sdd-docs-playbook/`.
If you have no access to the library files, stop. Ask the user to give access by the library file `en/README.md`, section "Preparation". Do not write the text of library files from memory.
If the file already exists in `docs/`, stop and ask the user.

## Step 3. Collect candidates

If `docs/_setup/inventory.md` lists a glossary or a section with terms, read it first. Take the first candidates from it.

For each area:
1. Read the specification of the area, if it exists.
2. Open the main domain classes (entities, services, DTOs).
3. Write down the nouns that repeat in the specification and in class names.

Do not write down general technical words: "service", "controller", "repository", "request", "response".
Write down domain words. Examples:
- book loans: reader, loan, return, fine;
- catalog: book, author, shelf.

## Step 4. Find synonyms and conflicts

For each candidate:
1. Find other words with the same meaning in specifications, code, comments, and README files.
   These are synonyms. They must be forbidden.
2. Check whether the word has two different meanings.
   This is a conflict. The user resolves it.

## Step 5. Fill in the glossary

Follow the instructions at the top of `docs/glossary.md`. Do not delete these instructions.

## Step 6. Verify the glossary

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Use only the "Glossary (if changed)" block. Fix all "no" items.

**STOP.** Show `docs/glossary.md` to the user. Show all conflicts in a separate list. For each conflict, propose 2 solutions. Format:

```
Word: <word>
Meanings: <meaning 1>; <meaning 2>
Option 1: <solution>
Option 2: <solution>
```

Wait for the decisions.

## Step 7. Finish the stage

1. Fix the glossary by the decisions of the user.
2. Mark stage 02 in `docs/_setup/progress.md`.
