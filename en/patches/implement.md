# Patch for an implementation skill

Skill type: implementation. To determine the type and apply the patch, see `en/patches/README.md`.

## Where to insert

Insert the text as the last step before the skill completes.
If the skill prints a final report, insert the text before that step.

## Patch text

```markdown
- Before completion, run the `docs-sync` skill. If the project does not have this skill, update the guides by `docs/DOCS-RULES.md`, section 6 "How to update".
```
