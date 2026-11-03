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
