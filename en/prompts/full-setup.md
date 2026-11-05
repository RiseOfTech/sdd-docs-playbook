# Task: add readable documentation to the project and keep it up to date

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the stages in order.

---

## 0. Main rules (always follow them)

1. Do the stages strictly in order. Do not skip stages.
2. After each stage, update the file `docs/_setup/progress.md`.
3. At steps marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
4. Do not change the program code. You work only with documentation and instructions.
5. Do not change the format of existing specifications. You can only read specifications.
6. Do not invent names of classes, methods, files, or fields.
   Copy each name in the documentation from a file that you opened in this session.
7. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the text. Do not guess.
8. Work on one area (capability) at a time. Do not keep several areas in progress.
9. Do not make commits or create branches unless the user asks.
10. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.
11. If the documentation root is not `docs/` (step 1.0), replace `docs/` with the documentation root in all paths and texts of this prompt.

**If the work was interrupted:** open `docs/_setup/progress.md`. If the file does not exist, find the file `_setup/progress.md` in the project. Continue from the first step that is not finished.

---

## 1. What you build

The mechanism has seven parts:

| No. | Part | File | Purpose |
|---|---|---|---|
| 1 | Rules | `docs/DOCS-RULES.md` | Single rules for writing and maintenance. All skills and agents link to this file. |
| 2 | Map | `docs/MAP.md` | Project areas and the documents for each area. A person who does not know the project starts with this file. |
| 3 | Route | `docs/ONBOARDING.md` | What each role reads and in which order. |
| 4 | Glossary | `docs/glossary.md` | Project terms. One term = one meaning. |
| 5 | Guides | `docs/guide/<area>/analyst.md` and `dev.md` | Short explanations for the analyst and the developer. |
| 6 | Templates | `docs/guide/_template/` | Guide templates. |
| 7 | Integration | skill / agent rules / SDD config | Makes sure that guides are updated with each change. |

Main idea: **the rules are written once, in `docs/DOCS-RULES.md`.**
Skills, configs, and agent instructions do not copy the rules. They only link to this file.

---

## Stage 1. Explore the project

Goal: understand what the project is and which tools it already has.
Create nothing except the report files.

### Step 1.0. Choose the documentation root

The documentation root is the folder that holds all documentation files. By default, it is `docs/`.

1. Check the project root. Find folders with `.md` files, for example `docs/`, `documentation/`, `wiki/`.
2. If there is no `docs/` folder but another documentation folder exists, stop. Ask the user: "The project documentation is in `<folder>/`. Create the documentation files in it or in a new `docs/` folder?"
3. Write down the answer. This is the documentation root.
4. If the documentation root is not `docs/`, replace `docs/` with the documentation root in all paths and texts of this prompt. Example: `docs/_setup/inventory.md` becomes `documentation/_setup/inventory.md`.

In all other cases, the documentation root is `docs/`.

### Step 1.1. Find files and write down what you found

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

### Step 1.2. Read the skills, rules, and documents that you found

For each skill and rules file, write one line:
`<path> — <what it does> — <when it runs>`.

Mark the skills that relate to: review, tasks, specifications, documentation.

For each document from the "Documentation" item of step 1.1, choose an assessment:
- "current" — the facts from the document match the code;
- "partly outdated" — some facts do not match the code;
- "outdated" — the document describes behavior or a process that no longer exists;
- "unknown" — you could not check the facts.

To choose the assessment, check 2–3 facts from the document against the code: class names, settings, dependencies. Write down the reason: which fact matched or did not match.

### Step 1.3. Define the areas (capabilities)

- If `openspec/specs/<name>/` exists, each folder = one area.
- If the project has another SDD tool, use its division.
- If the project has no SDD tool, add a question for the user: "The library is for projects with SDD. No SDD tool was found in the project. Continue?" Propose areas by modules or packages of business logic.
- If the specifications are divided by work stages, not by areas, do not use their division. Propose areas by the code. Add a question for the user.

Write down the list of areas. For each area: name, path to the specification (if any), paths to the code.

Paths to the code:
- If the area has its own folder or package, write down the path to it.
- If the code is divided by layers (for example, `controller`, `service`, `repository`), all areas have the same packages. Then for each layer, write down the files of the area or a name mask. Example for the library service: `service/Loan*`, `repository/LoanRepository.java`.
- Each path belongs to only one area. If two areas need one file, add a question for the user.

### Step 1.4. Write the report

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

If the project language does not match the language of this prompt, add a question: which language to use for the documentation. For Russian, use `ru/prompts/full-setup.md`. For English, use `en/prompts/full-setup.md`.

Create `docs/_setup/progress.md`:

```markdown
# Adoption progress

Documentation root: `<folder>/`

- [x] Stage 1. Explore the project
- [ ] Stage 2. Integration plan
- [ ] Stage 3. Rules and templates
- [ ] Stage 4. Map
- [ ] Stage 5. Glossary
- [ ] Stage 6. Pilot guides
- [ ] Stage 7. Other guides
- [ ] Stage 8. Integration into the process
- [ ] Stage 9. Final check

## Areas
| Area | analyst.md | dev.md | Verified |
|---|---|---|---|
```

**STOP.** Show `inventory.md` to the user. Ask the questions from the "Questions for the user" section. Wait for an answer.

---

## Stage 2. Integration plan

Goal: decide how the mechanism connects to what already exists.

### Step 2.1. Decide for each existing skill

For each skill that relates to review, tasks, specifications, or documentation, choose one action:

| Action | When to choose it |
|---|---|
| **Keep** | The skill does not touch documentation. |
| **Add a link** | The skill reviews work or closes tasks. Add 1–3 lines to it: "Check the guides by `docs/DOCS-RULES.md`, section 7 "Verification"". |
| **Replace** | The skill already creates similar documentation, but of lower quality. Propose a replacement. Do not delete it yourself. |

Rule for mixing skills:
- Do not copy the text of the rules into other skills. Give only a link to `docs/DOCS-RULES.md`.
- One skill = one task. Do not combine code review and guide writing in one skill.
- If two skills contradict each other, write the contradiction in the plan. Do not fix it yourself.

### Step 2.2. Decide where to integrate guide updates

Choose all rows of the table that apply.

| If the project has | Integrate like this |
|---|---|
| `openspec/config.yaml` | Add `context` and `rules` (the text is in stage 8). |
| Another SDD tool with a task template | Add the items from stage 8.1, the `tasks` key, to the task template. Write the path to the template file in the plan. |
| `AGENTS.md`, `CLAUDE.md`, or `GIGACODE.md` | Add a short section with a link to `docs/DOCS-RULES.md`. |
| A skills folder | Create the `docs-sync` and `docs-review` skills (the text is in stage 8). The folder name depends on the tool: Claude Code — `.claude/skills/`, GigaCode — `.gigacode/skills/`, OpenCode — `.opencode/skills/`, a shared folder — `.agents/skills/`. |

If the project has no SDD tool, stop. Tell the user: "The library is for projects with SDD. No SDD tool was found in the project." Wait for the decision of the user.

### Step 2.3. Write the plan

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

## Pilot area
<one area for stage 6 and why: medium size, has a specification, clear code>
```

**STOP.** Show the plan. Wait for a confirmation or changes.

---

## Stage 3. Rules and templates

Goal: create the rules file and the guide templates. Copy the texts below without changes.

### Step 3.1. Create `docs/DOCS-RULES.md`

Copy this text:

````markdown
# Project documentation rules

This file is the single source of rules. Skills and agents refer to it.

Do not change the section numbers. Skills and configs refer to them.
Refer to a section like this: section 7 "Verification".

## 1. Structure

- Project map: `docs/MAP.md`. A new person starts with this file.
  The map also shows which area a code path belongs to. One path belongs to one area.
- Reading route by role: `docs/ONBOARDING.md`.
- Glossary: `docs/glossary.md`.
- Guides: `docs/guide/<area>/analyst.md` and `docs/guide/<area>/dev.md`.
- Templates: `docs/guide/_template/`.

## 2. Writing rules

1. One sentence = one action or one fact.
2. A sentence has no more than 20 words. The maximum is 25.
3. Write in the active voice.
   - Bad: "The book is saved to the database."
   - Good: "`BookRepository` saves the book to the database."
4. For domain concepts, use only terms from `docs/glossary.md`. Use them with the meaning from the glossary.
5. Do not replace a term with a synonym. Repeating a term is normal.
6. Write names of classes, methods, files, and tables in `backticks`.
7. Write a condition like this: `If <condition>, <who> <action>.`
8. Write a warning like this: the command first, then the reason.
   - "Do not call `save()` in a loop. This creates many database queries."
9. A guide fits on one screen (about 60 lines). If it is longer, split the area.
10. Do not write filler phrases: "it should be noted", "in terms of", "utilize", "the aforementioned".
11. If a fact is not verified, write `[VERIFY: <what>]`.
12. Do not put code longer than 5 lines in a guide. Give a link to the class. Copied code becomes outdated first.

## 3. Two types of guides

| | `analyst.md` | `dev.md` |
|---|---|---|
| Reader | Analyst | Developer |
| Answers the question | What and why? | How and where? |
| Class names | No | Yes |
| Sections | Purpose, Business rules, Example | Entry point, How it works, How to change, Warnings |

Each guide has a verification line under its title:

```markdown
> Verified: 2026-10-31, commit `a1b2c3d`
```

The date is the day of the verification. Get the hash with `git rev-parse --short HEAD`.

## 4. Glossary

1. One term = one meaning.
2. Add a new term to the glossary first. Only then use it.
3. If a word has two meanings in the project, make two compound terms.
   Example: not "number", but "book number" and "reader number".
4. List forbidden synonyms in the "Do not use" column.
5. Do not delete a term if specifications or guides use it.
6. If a term is renamed, replace it in all guides. Add the old name to the "Do not use" column.
   In specifications, replace the term through the normal specification change process.

## 5. When to update

Update the guides of an area if one of these changed:
- a requirement in the specification of the area;
- an entry point, the order of steps, or conditions in the code;
- the name of a class or method that the guide mentions;
- a term in the glossary.

Update `docs/MAP.md` if one of these changed:
- the list of areas or their names;
- the path to the specification, code, or guide of an area;
- the owner of an area.

Update `docs/ONBOARDING.md` if:
- an area important for a new person is added;
- a guide from the reading route is deleted or renamed.

## 6. How to update

1. Find the changed areas:
   - if the specifications have a folder for the current change, use it;
   - otherwise, run `git diff --name-only <base>` and find the areas in `docs/MAP.md`;
   - if you cannot find the areas, ask the user.

   `<base>` is the branch where the work started. For example, `main`.
2. Find new domain words. Add them to the glossary.
3. Change only the affected sections of the guides.
4. Remove the description of deleted behavior from the guides.
5. Update `docs/MAP.md` and `docs/ONBOARDING.md` by section 5 "When to update".
6. Do section 7 "Verification". Fix all "no" items.
7. Update the "Verified" line in each changed guide.

## 7. Verification

Check each changed file against the list. For each item, write "yes" or "no + where".

**Link to the code (dev.md):**
- [ ] For each name in `backticks`: I opened the file and found this name.
- [ ] The "How it works" steps have the same order as the code.
- [ ] The "If ..." conditions match the conditions in the code.

**Link to the specification (analyst.md):**
- [ ] "Business rules" include each requirement of the specification.
- [ ] "Business rules" include no rule that is absent from the specification or the code.

**Terms (both guides):**
- [ ] The glossary has all domain words.
- [ ] There are no words from the "Do not use" column.
- [ ] Each term has the meaning from the glossary.

**Style (both guides):**
- [ ] Each sentence has no more than 25 words.
- [ ] One step = one action.
- [ ] `analyst.md` has no class names.
- [ ] The guide is no longer than ~60 lines.
- [ ] There is no code longer than 5 lines.
- [ ] There are no `[VERIFY]` marks (or you gave them to the user).

**Glossary (if changed):**
- [ ] A new term has a definition and a filled "In code" column.
- [ ] A new term does not duplicate an existing term.
- [ ] No guide has words from the "Do not use" column.

**Map (`docs/MAP.md`):**
- [ ] The map has each changed area.
- [ ] Links and paths in the map lead to existing specifications, guides, and code folders.
- [ ] Each changed area has an owner.

**Route (`docs/ONBOARDING.md`, if changed):**
- [ ] Links in the route lead to existing guides.

## 8. Report after the update

```
Areas: <list>
Changed files: <list>
New terms: <list or "none">
Map: <changed / no>
Glossary: <changed / no>
Verification: <all items "yes" or a list of "no + where">
Questions: <list or "none">
```
````

### Step 3.2. Create `docs/guide/_template/analyst.md`

````markdown
<!--
Instructions for the person or AI agent who fills in the guide.
The Markdown preview hides this block.

1. Copy this file to `docs/guide/<area>/analyst.md`.
2. Fill in the sections from the facts and the specification of the area. Replace all `<...>`. Keep backticks only around the commit hash.
3. Follow section 2 "Writing rules" and section 3 "Two types of guides" of `docs/DOCS-RULES.md`.
4. Delete this comment.

Guide example:

# Book loans — for the analyst

> Verified: 2026-10-31, commit `a1b2c3d`

## Purpose
The area lends a book to a reader and takes the book back. The librarian uses the result.

## Business rules
1. A reader gets a book for 14 days.
2. If a reader has an unpaid fine, the librarian does not lend a book.

## Example
A reader gets a book on March 1. → Return date: March 15.
-->

# `<Area>` — for the analyst

> Verified: `<YYYY-MM-DD>`, commit `<hash>`

## Purpose
`<1–3 sentences. What the area does. Who uses the result.>`

## Business rules
1. `<One rule — one sentence.>`
2. If `<condition>`, `<who>` `<action>`.

## Example
`<Specific input data.>` → `<Specific result.>`
````

### Step 3.3. Create `docs/guide/_template/dev.md`

````markdown
<!--
Instructions for the person or AI agent who fills in the guide.
The Markdown preview hides this block.

1. Copy this file to `docs/guide/<area>/dev.md`.
2. Fill in the sections from the facts. Replace all `<...>`. Keep backticks only around names from the code and the commit hash.
3. Write each "How it works" step as one line of the call chain.
4. Copy class and method names from files that you opened. Do not invent names.
5. Follow section 2 "Writing rules" and section 3 "Two types of guides" of `docs/DOCS-RULES.md`.
6. Delete this comment.

Guide example:

# Book loans — for the developer

> Verified: 2026-10-31, commit `a1b2c3d`

## Entry point
`LoanController.createLoan()`

## How it works
1. `LoanController.createLoan()` receives the book number and the reader number.
2. `LoanService.checkFines()` checks the fines of the reader.
3. If the reader has an unpaid fine, `LoanService` rejects the loan.
4. `LoanRepository.save()` saves the loan.

## How to change
- To change the loan period: change `LoanPolicy`. Then update the business rules in `analyst.md`.

## Warnings
- Do not call `LoanRepository.save()` directly. Only `LoanService` checks fines before the save.
-->

# `<Area>` — for the developer

> Verified: `<YYYY-MM-DD>`, commit `<hash>`

## Entry point
`<Class.method()>`

## How it works
1. `<Class>` `<one action>`.
2. `<Class.method()>` `<one action>`.
3. If `<condition>`, `<Class>` `<action>`.

## How to change
- To `<goal>`: change `<Class>`. Then `<next step>`.

## Warnings
- `<Command.>` `<Reason.>`
````

Mark stage 3 in `progress.md`.

---

## Stage 4. Map

Goal: show the project areas and the documents for each area.

### Step 4.1. Create `docs/MAP.md`

Copy this text:

````markdown
<!--
Instructions for the person or AI agent who fills in the map.
The Markdown preview hides this block.

1. Open `docs/_setup/inventory.md` if it exists. Take the list of areas from it.
2. Group the areas into blocks. The block name answers the question: what will the reader understand?
3. Put blocks and areas in reading order: from the general picture to the details.
4. Copy the block section as many times as necessary. Replace all `<...>`. Keep backticks only around area names and paths.
5. Copy paths from folders that you opened. Do not invent paths.
6. If an area has no specification or guide, write "none" in the cell.
7. If the file `docs/ONBOARDING.md` does not exist, delete its row from the "Where to find the answer" table.
8. If the folder `docs/_setup/` does not exist, delete the "Folder `docs/_setup/`" section.
9. Delete this comment.

Block example:

## Block 2. How a book reaches the reader

| Area | Purpose | Code | Specification | Guides | Owner |
|---|---|---|---|---|---|
| `book-loan` | Lends a book to a reader and takes the book back. | `src/loans/` | `openspec/specs/book-loan/` | [analyst](guide/book-loan/analyst.md), [dev](guide/book-loan/dev.md) | Loans team |
| `loan-fines` | Charges a fine for a late return. | `src/fines/` | none | none | Loans team |
-->

# Project map

`<1–2 sentences: what the project does and who uses the result.>`

The map shows the project areas and the documents for each area.
How to maintain the map: `docs/DOCS-RULES.md`, section 5 "When to update".

## Where to find the answer

| Question | Where is the answer |
|---|---|
| Where do I start? | `docs/ONBOARDING.md` |
| What does a term mean? | `docs/glossary.md` |
| What does an area do and why? | `analyst.md` of the area |
| How does an area work and where do I change it? | `dev.md` of the area |
| Which area does a file belong to? | The "Code" column in the tables below |
| Who confirms that a guide is correct? | The "Owner" column in the tables below |

Blocks and areas are in reading order.

## Block 1. `<What the reader will understand>`

| Area | Purpose | Code | Specification | Guides | Owner |
|---|---|---|---|---|---|
| `<area>` | `<One sentence.>` | `<path to code>` | `<path to specification>` | [analyst](guide/<area>/analyst.md), [dev](guide/<area>/dev.md) | `<Person or team>` |

## Service areas

These areas have no business rules. Read them with `dev.md`.

| Area | Purpose | Code | Specification | Guides | Owner |
|---|---|---|---|---|---|
| `<area>` | `<One sentence.>` | `<path to code>` | `<path to specification>` | [dev](guide/<area>/dev.md) | `<Person or team>` |

## Other documents

| Document | When to open it | What it gives |
|---|---|---|
| `<path to document>` | `<When you need this document.>` | `<One sentence.>` |

## Folder `docs/_setup/`

You do not need to read this folder. It has no guides or rules.
The folder holds the working files of the AI agent that analyzed the code and created the documentation: the list of areas, the work plan, the progress notes.
````

### Step 4.2. Fill in the map

Follow the instructions at the top of `docs/MAP.md`. Apply these conditions:

- Keep the `docs/ONBOARDING.md` row in the "Where to find the answer" table. The file appears at stage 6.
- In the "Guides" column, write "none". Guides appear at stages 6 and 7.
- If the owner of an area is unknown, write `[VERIFY: area owner]`.
- If there are no service areas, delete the "Service areas" section.
- Fill in the "Other documents" section from the "Existing documentation" section of `inventory.md`. If there are no documents, delete the section.

### Step 4.3. Verify the map

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Use only the "Map (`docs/MAP.md`)" block. Fix all "no" items.

Add each area to the "Areas" table in `progress.md`.

**STOP.** Show `docs/MAP.md`. Show all `[VERIFY]` marks in a separate list. Ask:
1. Are the block names clear?
2. Is the reading order correct?
3. Who owns the areas without an owner?

Wait for an answer. After the answer, fix the map. Mark stage 4 in `progress.md`.

---

## Stage 5. Glossary

Goal: collect the project terms.

### Step 5.1. Collect candidates

If `docs/_setup/inventory.md` lists a glossary or a section with terms, read it first. Take the first candidates from it.

For each area:
1. Read the specification of the area, if it exists.
2. Open the main domain classes (entities, services, DTOs).
3. Write down the nouns that repeat in the specification and in class names.

Do not write down general technical words: "service", "controller", "repository", "request", "response".
Write down domain words. Examples:
- book loans: reader, loan, return, fine;
- catalog: book, author, shelf.

### Step 5.2. Find synonyms and conflicts

For each candidate:
1. Find other words with the same meaning in specifications, code, comments, and README files.
   These are synonyms. They must be forbidden.
2. Check whether the word has two different meanings.
   This is a conflict. The user resolves it.

### Step 5.3. Create a draft of `docs/glossary.md`

Copy this text. Then follow the instructions at its top. Do not delete these instructions.

````markdown
<!--
Instructions for the person or AI agent who adds a term.
Read them before you edit the table. Do not delete this block.
The Markdown preview hides this block so that it does not interrupt reading the glossary.

1. Add one row to the table for each term.
2. Fill in the columns by the list below. Keep backticks only in the "In code" column.
3. Sort the terms alphabetically.
4. Delete the placeholder row.

Columns:

- Term: with a capital letter, in the base form.
- Definition: 1–2 short sentences. Write by section 2 "Writing rules" of `docs/DOCS-RULES.md`. Do not refer to code.
- In code: the main class. Copy the name from a file that you opened. If there is no class, write `—`.
- Do not use: synonyms separated by `;`.
- Note: if there is a conflict, describe it and propose a solution. If there is no conflict, leave the cell empty.

Table example:

| Term | Definition | In code | Do not use | Note |
|---|---|---|---|---|
| Book number | The unique number of a book in the catalog. | `BookNumber` | Number | |
| Fine | The amount that a reader pays for a late return. | `Fine` | Penalty | Conflict: the specification also calls a reader block a fine. Solution: add the term "Reader block". |
| Loan | The library gives a book to a reader for a period. | `Loan` | Rental; Borrowing | |
| Reader number | The unique number of a reader in the library. | `ReaderNumber` | Number | |
| Return | A reader gives a book back to the library. | — | Hand-in | |
-->

# Project glossary

Glossary rules: `docs/DOCS-RULES.md`, section 4 "Glossary".

| Term | Definition | In code | Do not use | Note |
|---|---|---|---|---|
| `<Term>` | `<1–2 short sentences.>` | `<Class>` or — | `<synonym>`; `<synonym>` | `<conflict or empty>` |
````

### Step 5.4. Verify the glossary

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Use only the "Glossary (if changed)" block. Fix all "no" items.

**STOP.** Show the glossary. Show all conflicts in a separate list. For each conflict, propose 2 solutions. Format:

```
Word: <word>
Meanings: <meaning 1>; <meaning 2>
Option 1: <solution>
Option 2: <solution>
```

Wait for the decisions.

After the answer, fix the glossary. Mark stage 5 in `progress.md`.

---

## Stage 6. Pilot guides

Goal: create guides for one area. The user checks the quality before the mass work.

### Step 6.1. Collect the facts for the pilot area

1. Read the whole specification of the area, if it exists.
2. Find the entry point: a controller, a scheduled task, a message listener, a public method.
3. Follow the code from the entry point. Write down the call chain: `Class.method()` → `Class.method()`.
4. Write down all conditions (`if`, `switch`, exceptions) that change the result.

Write the facts to `docs/_setup/facts-<area>.md`. This is a draft. The user does not read it.

### Step 6.2. Write `analyst.md`

If the area is in the "Service areas" section of `docs/MAP.md`, skip this step.

1. Copy `docs/guide/_template/analyst.md` to `docs/guide/<area>/analyst.md`.
2. Follow the instructions at the top of the file.

### Step 6.3. Write `dev.md`

1. Copy `docs/guide/_template/dev.md` to `docs/guide/<area>/dev.md`.
2. Follow the instructions at the top of the file.

### Step 6.4. Verify

Follow `docs/DOCS-RULES.md`, section 7 "Verification". Fix all "no" items.

### Step 6.5. Update the map and create the route

In `docs/MAP.md`, replace "none" in the "Guides" column with links to the guides of the area.

Create `docs/ONBOARDING.md`. Copy this text. Then follow the instructions at its top.

````markdown
<!--
Instructions for the person or AI agent who fills in the route.
The Markdown preview hides this block.

1. Open `docs/MAP.md`. Choose the areas that are important for a new person.
2. For each role, add one row for each guide of these areas.
3. Put the rows in reading order: from the general picture to the details.
4. Replace all `<...>`. Keep backticks only around paths and area names.
5. If the project has another role, copy a role section and change it.
6. Delete this comment.

Row example:

| Document | What to read | What it gives |
|---|---|---|
| [`book-loan`](guide/book-loan/analyst.md) | The whole file | Explains the rules for book loans and returns. |
-->

# Reading route

The route shows what a person who does not know the project reads, and in which order.
How to maintain the route: `docs/DOCS-RULES.md`, section 5 "When to update".

Find your role. Read the documents from top to bottom.

## Analyst

| Document | What to read | What it gives |
|---|---|---|
| `docs/MAP.md` | The whole file | Shows the project areas and their owners. |
| `docs/glossary.md` | The whole file | Explains the project terms. |
| [`<area>`](guide/<area>/analyst.md) | `<What to read.>` | `<One sentence.>` |
| `docs/DOCS-RULES.md` | Section 2 "Writing rules" | Shows how to write guides. |

## Developer

| Document | What to read | What it gives |
|---|---|---|
| `docs/MAP.md` | The whole file | Shows the project areas and the paths to the code. |
| `docs/glossary.md` | The whole file | Explains the project terms and their names in the code. |
| [`<area>`](guide/<area>/dev.md) | `<What to read.>` | `<One sentence.>` |
| `docs/DOCS-RULES.md` | Section 5 "When to update" | Shows when to update guides after a code change. |
````

**STOP.** Show both guides and the verification result. Ask:
1. Is `analyst.md` clear to an analyst?
2. Is `dev.md` enough for a developer to find the place to change?
3. What should change in the templates or rules?

If the user asks to change the templates or rules, change `docs/DOCS-RULES.md` and the templates. Then redo the pilot guides.

Mark stage 6 in `progress.md`.

---

## Stage 7. Other guides

For each remaining area, repeat steps 6.1–6.4. Then replace "none" in the "Guides" column of the map. Do not stop after each area.

Rules:
1. One area at a time. Finish the area, then start the next one.
2. After each area, update the "Areas" table in `progress.md`.
3. If you found a new term, add it to the glossary and mark it in the report.
4. If a guide is longer than 60 lines, propose to split the area. Do not split it yourself.
5. If an area is important for a person who does not know the project, add its rows to `docs/ONBOARDING.md`.
6. Every 5 areas, briefly tell the user how many are done and which questions have accumulated.

Mark stage 7 in `progress.md`.

---

## Stage 8. Integration into the process

Carry out the plan from `docs/_setup/plan.md`. Use the texts below. Do not copy the rules. Give only a link.

### 8.1. If `openspec/config.yaml` exists

Add to `context` (do not delete existing content):

```yaml
  Documentation: rules in docs/DOCS-RULES.md, glossary in docs/glossary.md.
  Use only terms from the glossary.
```

Add to `rules` (merge with existing rules):

```yaml
  proposal:
    - List the areas whose guides will change (docs/guide/<area>/).
  specs:
    - Use terms from docs/glossary.md with the meaning from the glossary.
  tasks:
    - Add a task to the end of the list - update the guides by docs/DOCS-RULES.md, section 6 "How to update".
    - After it, add a task - verify the guides by docs/DOCS-RULES.md, section 7 "Verification".
    - If another rule requires its own last task (for example, a build), put the guide tasks before it.
```

A rule about the last task (for example, "finish with a build") is not a contradiction. The third `tasks` item puts the guide tasks before that task.

### 8.2. If `AGENTS.md`, `CLAUDE.md`, or `GIGACODE.md` exists

GigaCode reads only `GIGACODE.md`. If the team works in GigaCode, add the section to `GIGACODE.md`, even if this file links to another file.

If the file has a section with the same purpose under a different name, ask the user: add the lines to that section or create a "Documentation" section. Example: a "References" section with links to project documents.

Add this section:

```markdown
## Documentation
- Rules: `docs/DOCS-RULES.md`. Glossary: `docs/glossary.md`.
- After a change to a specification or to code behavior, update the guides by `docs/DOCS-RULES.md`, section 6 "How to update".
- For domain concepts, use only terms from the glossary.
```

### 8.3. If a skills folder exists, create the `docs-sync` and `docs-review` skills

Path: `<skills folder>/docs-sync/SKILL.md`. Text:

```markdown
---
name: docs-sync
description: Updates the docs/guide guides, the docs/glossary.md glossary, and the docs/MAP.md map after changes to specifications or code. Then verifies the result. Use after implementing a change and on the request "update the documentation".
---

# docs-sync

## Main rules

1. Change only the files in the `docs/` folder. Do not change the program code or the specifications.
2. Do not invent names of classes, methods, files, or fields. Copy each name from a file that you opened in this session.
3. Do not make commits or create branches unless the user asks.

## Steps

1. Read `docs/DOCS-RULES.md` completely.
2. Read `docs/glossary.md`.
3. Read `docs/MAP.md`.

   If one of these files does not exist, stop. Tell the user which file does not exist.
4. Determine the changed areas by `docs/DOCS-RULES.md`, section 6 "How to update", item 1.
5. Compare the changes with `docs/DOCS-RULES.md`, section 5 "When to update".

   If there is nothing to update, do not change files. Go to step 7. In the "Areas" line, write "none".
6. Work on areas one at a time. For each area, follow `docs/DOCS-RULES.md`, section 6 "How to update", items 2-7.

   If an area has no guides, do not create them. Write the area in the "Questions" line of the report.
7. Print the report by `docs/DOCS-RULES.md`, section 8 "Report after the update".
```

Path: `<skills folder>/docs-review/SKILL.md`. Text:

```markdown
---
name: docs-review
description: Verifies the docs/guide guides, the docs/glossary.md glossary, and the docs/MAP.md map against the project rules. Changes nothing. Use before a review, before archiving a change, and on the request "check the documentation".
---

# docs-review

## Main rules

1. Change nothing. Only read files and run the `git diff` and `git log` commands.
2. Do not invent names of classes, methods, files, or fields. Copy each name from a file that you opened in this session.
3. Do not fix the errors you find. Only report them.

## Steps

1. Read `docs/DOCS-RULES.md` completely.
2. Read `docs/glossary.md`.
3. Read `docs/MAP.md`.

   If one of these files does not exist, stop. Tell the user which file does not exist.
4. Determine the changed areas by `docs/DOCS-RULES.md`, section 6 "How to update", item 1.
5. Compare the changes with `docs/DOCS-RULES.md`, section 5 "When to update".

   If a file needed an update and it did not change, write an error: "no + where".
   If an area has no guides, do not write an error about the guides. See step 6.
6. Work on areas one at a time. For each area, follow `docs/DOCS-RULES.md`, section 7 "Verification".

   If an area has no guides, this is not an error. Do not verify the guides of this area. Write the area in the "Questions" line of the report.
7. Print the report by `docs/DOCS-RULES.md`, section 8 "Report after the update". In the "Changed files" line, write "none".
8. Add the line `Result: <no errors / errors found>` at the end of the report. If there is at least one "no" item, write "errors found".
```

### 8.4. Existing skills

For each skill with the "Add a link" action in the plan, add one line to its steps.
Example for a task review skill:

```markdown
- Check the guides of the changed areas by `docs/DOCS-RULES.md`, section 7 "Verification". Add "no" items to the review remarks.
```

Do not change the rest of the skill text.

Special cases:
- The skill has other copies of its text. For example, the `.claude/commands/opsx/archive.md` command and the `.claude/skills/openspec-archive-change/SKILL.md` skill. GigaCode works the same way: the skill `.gigacode/skills/openspec-archive-change/SKILL.md` and a command in `.gigacode/commands/`. Add the line to each copy in the same way.
- A generator created the skill (the `generatedBy` field). The update command of the tool can delete the line. Tell the user: after you update the tool, check this line.
- The skill is outside the repository (for example, in `~/.claude/skills/`). Do not change it. Tell the user which line to add. The user gives it to the owner of the skill.

### 8.5. README

Add this section to `README.md`:

```markdown
## Documentation
- Project map: `docs/MAP.md`.
- How the project works for the analyst and the developer: `docs/guide/`.
- Terms: `docs/glossary.md`.
- Maintenance rules: `docs/DOCS-RULES.md`.
```

Mark stage 8 in `progress.md`.

---

## Stage 9. Final check

1. For each area, check that `dev.md` exists. For areas outside the "Service areas" section, check that `analyst.md` exists.
2. Choose 3 random guides. Follow `docs/DOCS-RULES.md`, section 7 "Verification", for them again.
3. Check that each changed skill and config links to `docs/DOCS-RULES.md` and does not copy the rules.
4. Collect all `[VERIFY]` marks from the guides into one list.
5. Delete the drafts `docs/_setup/facts-*.md`. Keep `inventory.md`, `plan.md`, and `progress.md`.

Print the final report:

```
Created: <files>
Changed: <files and what was added>
Areas: <N>, guides: <M>
Terms in the glossary: <N>
Open questions ([VERIFY] and conflicts): <list>
How to work from now on:
  - after a change: <command or skill>
  - for a review: <command or skill>
```

Mark stage 9 in `progress.md`.
