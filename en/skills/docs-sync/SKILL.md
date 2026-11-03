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
