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
