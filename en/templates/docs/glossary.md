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
