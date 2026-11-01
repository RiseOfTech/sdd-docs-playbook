# Integration with OpenSpec

Use this file if the project has `openspec/config.yaml`.

Goal: OpenSpec creates each change with tasks to update and verify the guides.
Do not copy the rules. Give only a link to `docs/DOCS-RULES.md`.

## Step 1. Add the text to `context`

1. Open `openspec/config.yaml`.
2. Find the `context` key.
3. Add this text to the end of the value. Do not delete the existing text.

```yaml
  Documentation: rules in docs/DOCS-RULES.md, glossary in docs/glossary.md.
  Use only terms from the glossary.
```

If the `context` key does not exist, create it as `context: |`. Then add the text under it.

## Step 2. Add the text to `rules`

1. Find the `rules` key.
2. Add these items. Do not delete the existing items.

```yaml
  proposal:
    - List the areas whose guides will change (docs/guide/<area>/).
  specs:
    - Use terms from docs/glossary.md with the meaning from the glossary.
  tasks:
    - The next-to-last task is to update the guides by docs/DOCS-RULES.md, section 6 "How to update".
    - The last task is to verify the guides by docs/DOCS-RULES.md, section 7 "Verification".
```

If the `rules` key does not exist, create it. Then add the text under it.

## How to merge with existing text

1. If `rules` already has `proposal`, `specs`, or `tasks`, do not create a second key with that name. Add the items to the end of the existing list.
2. If a new item contradicts an existing item, do not change the existing item. Ask the user.
3. Keep the indentation of the file. YAML does not work with wrong indentation.
4. Do not change other keys of the file.

Example for the library service.

Before:

```yaml
context: |
  Library service: books, readers, loans.

rules:
  tasks:
    - Each task changes one area.
```

After:

```yaml
context: |
  Library service: books, readers, loans.
  Documentation: rules in docs/DOCS-RULES.md, glossary in docs/glossary.md.
  Use only terms from the glossary.

rules:
  proposal:
    - List the areas whose guides will change (docs/guide/<area>/).
  specs:
    - Use terms from docs/glossary.md with the meaning from the glossary.
  tasks:
    - Each task changes one area.
    - The next-to-last task is to update the guides by docs/DOCS-RULES.md, section 6 "How to update".
    - The last task is to verify the guides by docs/DOCS-RULES.md, section 7 "Verification".
```
