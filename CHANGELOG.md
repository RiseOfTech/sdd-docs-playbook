# Changelog

**[English](#english)** | **[Русский](#русский)**

## English

### 0.1.1 — 2026-11-05

Support for GigaCode and for a documentation folder with a different name.

- A documentation root. If the project documentation is in a different folder, for example `documentation/`, the prompt `00-explore.md` asks the user where to create the files. The other prompts read the answer from `_setup/progress.md`.
- GigaCode: access to the library through `/dir add`, the skills folder `.gigacode/skills/`, the commands folder `.gigacode/commands/`. GigaCode reads only `GIGACODE.md`, so the "Documentation" section goes into this file.
- Agent instruction files: a rule for a section with the same purpose under a different name.
- README: the library folder must have the name `sdd-docs-playbook`, also after you unpack the ZIP archive.

### 0.1.0 — 2026-11-03

The first version.

- Templates for the `docs/` folder: the rules `DOCS-RULES.md`, the map `MAP.md`, the route `ONBOARDING.md`, the glossary `glossary.md`, the guide templates `analyst.md` and `dev.md`.
- Prompts for an agent: from `00-explore.md` to `05-audit.md`, and `full-setup.md` for a small project.
- The `docs-sync` (documentation update) and `docs-review` (documentation verification) skills.
- Patches for project skills: review, implementation, specification creation, archive.
- Integration with OpenSpec and with agent instruction files: `AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`.
- All files in Russian and English.

This version is tested on a real project with OpenSpec and Claude Code.

## Русский

### 0.1.1 — 2026-11-05

Поддержка GigaCode и папки документации с другим именем.

- Корень документации. Если документация проекта лежит в другой папке, например `documentation/`, промпт `00-explore.md` спрашивает пользователя, где создать файлы. Остальные промпты берут ответ из `_setup/progress.md`.
- GigaCode: доступ к библиотеке через `/dir add`, папка навыков `.gigacode/skills/`, папка команд `.gigacode/commands/`. GigaCode читает только `GIGACODE.md`, поэтому раздел "Документация" стоит в этом файле.
- Файлы инструкций агентов: правило для раздела с той же целью под другим именем.
- README: папка библиотеки должна называться `sdd-docs-playbook`, в том числе после распаковки ZIP-архива.

### 0.1.0 — 2026-11-03

Первая версия.

- Шаблоны для папки `docs/`: правила `DOCS-RULES.md`, карта `MAP.md`, маршрут `ONBOARDING.md`, словарь `glossary.md`, шаблоны гайдов `analyst.md` и `dev.md`.
- Промпты для агента: от `00-explore.md` до `05-audit.md` и `full-setup.md` для небольшого проекта.
- Навыки `docs-sync` (обновление документации) и `docs-review` (проверка документации).
- Патчи для навыков проекта: ревью, реализация, создание спецификации, архив.
- Интеграция с OpenSpec и с файлами инструкций агентов: `AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`.
- Все файлы на русском и английском языках.

Версия проверена на реальном проекте с OpenSpec и Claude Code.
