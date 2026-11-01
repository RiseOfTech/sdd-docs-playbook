<!--
How to fill in the map. The reader of the map does not see this comment.

1. Open `docs/_setup/inventory.md` if it exists. Take the list of areas from it.
2. Group the areas into blocks. The block name answers the question: what will the reader understand?
3. Put blocks and areas in reading order: from the general picture to the details.
4. Copy the block section as many times as necessary. Replace all `<...>`.
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

<1–2 sentences: what the project does and who uses the result.>

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

## Block 1. <What the reader will understand>

| Area | Purpose | Code | Specification | Guides | Owner |
|---|---|---|---|---|---|
| `<area>` | <One sentence.> | `<path to code>` | `<path to specification>` | [analyst](guide/<area>/analyst.md), [dev](guide/<area>/dev.md) | <Person or team> |

## Service areas

These areas have no business rules. Read them with `dev.md`.

| Area | Purpose | Code | Specification | Guides | Owner |
|---|---|---|---|---|---|
| `<area>` | <One sentence.> | `<path to code>` | `<path to specification>` | [dev](guide/<area>/dev.md) | <Person or team> |

## Other documents

| Document | When to open it | What it gives |
|---|---|---|
| `<path to document>` | <When you need this document.> | <One sentence.> |

## Folder `docs/_setup/`

You do not need to read this folder. It has no guides or rules.
The folder holds the working files of the AI agent that analyzed the code and created the documentation: the list of areas, the work plan, the progress notes.
