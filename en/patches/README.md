# Patches for existing skills

A patch is a short insert for a project skill. A patch connects the skill to `docs/DOCS-RULES.md`.
**DO NOT REPLACE PROJECT SKILLS.** Add only the patch to them.

## How to apply

1. Open the skills folder of the project. It is in the project root. The folder name depends on the tool:
   - Claude Code: `.claude/skills/`;
   - GigaCode: `.gigacode/skills/`;
   - OpenCode: `.opencode/skills/`;
   - shared folder for different agents: `.agents/skills/`.

   The names of these folders start with a dot. A file manager can hide them. Open the project in a code editor: these folders are visible there.
   If there is no such folder, ask the person responsible for the project development where the skills are.
2. Read the skill. Find its type in the table.
3. Open the file from the "Patch" column.
4. Insert the patch text into the steps of the skill.
5. Do not change the other text of the skill.
6. Find other copies of the skill text. For example, in Claude Code the `/opsx:archive` command is in `.claude/commands/opsx/archive.md`, and the archive skill is in `.claude/skills/openspec-archive-change/SKILL.md`. These are two copies of one text. Insert the patch into each copy in the same way.

If a skill fits two types, ask the user.
If a skill fits no type, leave it unchanged.

## Special cases

**A generator created the skill.** Sign: the skill has the `generatedBy` field or a note about generation. The update command of the tool can overwrite such a file and delete the patch. For example, `openspec update`.
1. After you update the tool, check that the patch is in place.
2. If the patch is not there, insert it again.

The rules from `en/integrations/openspec.md` are in `openspec/config.yaml`, not in the skill files. So an overwrite of the skills does not delete them.

**The skill is outside the repository.** For example, in `~/.claude/skills/`. Other projects can use such a skill.
1. Do not change this skill.
2. Tell the user which patch the skill needs.
3. The user gives the patch text to the owner of the skill.

## Type table

| Skill type | Sign | Patch | What the patch does |
|---|---|---|---|
| Code or task review | "review", "check", checklist | `review.md` | Adds a guide check to the review checklist. |
| Implementation | "implement", "apply", runs tasks | `implement.md` | Adds a `docs-sync` call before completion. |
| Specification creation | "propose", "spec", "new change" | `propose.md` | Requires terms from the glossary and a list of areas whose guides will change. |
| Archive or completion | "archive", "done", "release" | `archive.md` | Forbids the archive if `docs-review` found errors. |
| The necessary skill does not exist | — | — | No patch is necessary. Take a new skill from `en/skills/`. |

## Patch rules

1. A patch is 1–3 lines and a link to `docs/DOCS-RULES.md`.
2. Do not copy rules into a patch.
3. One skill = one task. Do not combine code review and guide writing in one skill.
4. If two skills contradict each other, tell the user. Do not fix this yourself.
