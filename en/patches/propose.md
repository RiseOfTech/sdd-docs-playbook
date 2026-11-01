# Patch for a specification creation skill

Skill type: specification creation. To determine the type and apply the patch, see `en/patches/README.md`.

## Where to insert

Insert the text into the step where the skill writes the specification or the change description.
If there is no such step, insert the text as the last step before the result output.

## Patch text

```markdown
- For domain concepts, use only terms from `docs/glossary.md`. Rules: `docs/DOCS-RULES.md`, section 4 "Glossary".
- In the change description, list the areas whose guides will change (`docs/guide/<area>/`). Copy the area names from `docs/MAP.md`.
```
