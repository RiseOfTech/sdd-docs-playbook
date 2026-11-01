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
