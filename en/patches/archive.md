# Patch for an archive skill

Skill type: archive or completion. To determine the type and apply the patch, see `en/patches/README.md`.

## Where to insert

Insert the text as the first step of the skill. This step must come before the archive.

## Patch text

```markdown
- Before the archive, run the `docs-review` skill. If the report has "Result: errors found", do not archive. Show the errors to the user.
- If the project does not have this skill, check the guides by `docs/DOCS-RULES.md`, section 7 "Verification". If there are "no" items, do not archive. Show them to the user.
```
