# Task: check that the documentation is not outdated

You are an AI agent. You work in the project repository.
Read this instruction completely. Then do the steps in order.

Run this prompt once a month or once a quarter.

Goal: find guides that drifted away from the code or the specification.
Result: a report for the user. Do not change guides at this stage.

## Main rules

1. Do the steps strictly in order. Do not skip steps.
2. At a step marked **STOP**, show the result to the user. Wait for an answer. Do not continue without an answer.
3. Change nothing. Only read files and run the `git log` command.
4. Do not invent file names or commit hashes. Copy them from command output and opened files.
5. If you are not sure about a fact, write `[VERIFY: <what exactly>]` in the report. Do not guess.
6. If this instruction contradicts the project rules (`AGENTS.md`, `CLAUDE.md`, `GIGACODE.md`, and so on), stop and ask the user.

**Documentation root.** This is the folder with the files `MAP.md` and `DOCS-RULES.md`, usually `docs/`. If the file `docs/MAP.md` does not exist, find the file `MAP.md` next to `DOCS-RULES.md` in the project. In all paths of this prompt, replace `docs/` with this folder.

## Step 1. Collect the list of guides

1. Open `docs/MAP.md`.
2. For each area, write down: paths to the code, path to the specification, paths to the guides.

If the file `docs/MAP.md` does not exist, stop. Tell the user: "Run the prompt `01-map.md` first."

## Step 2. Find outdated guides

For each guide:

1. Open the guide. Find the "Verified" line. Copy the date from it.
2. Find the last commit that changed the guide:

   ```
   git log -1 --format=%h -- <path to guide>
   ```

3. Find the commits after it. Use the hash from item 2 and the paths of the area:

   ```
   git log --oneline <hash>..HEAD -- <path to code> <path to specification>
   ```

4. If the output is empty, the guide is not outdated. Go to the next guide.
5. If the output has commits, the guide is outdated.

Do not use the hash from the "Verified" line. After a squash or a rebase, that commit may not be in the history.

## Step 3. Find marks

Find all `[VERIFY]` marks in the folder `docs/guide/`. Skip the folder `docs/guide/_template/`.

## Step 4. Find areas without guides

In `docs/MAP.md`, find the areas that have "none" in the "Guides" column.

## Step 5. Print the report

```
Date: <YYYY-MM-DD>
Guides checked: <N>

Outdated guides:
| Guide | Verified | Commits |
|---|---|---|

[VERIFY] marks:
<file — text of the mark, or "none">

Areas without guides:
<list or "none">
```

**STOP.** Show the report. Ask the user which guides to update. Do not update them yourself.
