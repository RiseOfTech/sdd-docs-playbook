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
