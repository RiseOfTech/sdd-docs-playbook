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
6. Work on areas one at a time. For each area, follow `docs/DOCS-RULES.md`, section 7 "Verification".
7. Print the report by `docs/DOCS-RULES.md`, section 8 "Report after the update". In the "Changed files" line, write "none".
8. Add the line `Result: <no errors / errors found>` at the end of the report. If there is at least one "no" item, write "errors found".
