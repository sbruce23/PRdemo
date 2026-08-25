# Resolving merge conflicts intentionally

A merge conflict is not an error message to erase. It is a request for a human decision: Git found overlapping changes and cannot infer the intended combined result.

## Before editing

1. Read the pull request and both competing changes.
2. State in plain language what the final file should contain.
3. Decide whether the conflict is simple enough for GitHub's web editor.

Use the GitHub interface only for a small text conflict whose final result is obvious and requires no local test. Resolve code, notebooks, multiple files, generated files, or test-sensitive changes locally.

## Simple conflict in the GitHub interface

1. Open the conflicted pull request.
2. Select **Resolve conflicts**.
3. Compare the sections between `<<<<<<<`, `=======`, and `>>>>>>>`.
4. Edit the file to the intended final content. Remove all conflict markers.
5. Select **Mark as resolved**, then **Commit merge**.
6. Return to **Files changed** and review the complete result before merge.

## Local fallback for a conflict on `dev`

From the contributor's clone:

```bash
cd ~/stat315/PRdemo
git switch dev
git status
git fetch upstream
git merge upstream/main
```

If Git reports a conflict, list and inspect the affected files:

```bash
git status
git diff --name-only --diff-filter=U
git diff
```

Edit each conflicted file to the intended final content. Do not merely delete the marker lines while leaving contradictory content. Then verify, stage, commit, and update the same pull request:

```bash
git diff --check
git add fav_animal.txt
git diff --staged
git commit -m "Resolve upstream merge conflict"
git push origin dev
```

The existing pull request updates automatically.

## Safe abort path

If you started the merge on the wrong branch or do not yet understand the intended result, stop before committing:

```bash
git merge --abort
git status
```

Ask for clarification, then begin again from a known state. Aborting is safer than guessing.

## Verification questions

- Does `git status` show no unmerged paths?
- Does `git diff --check` report no conflict markers or whitespace errors?
- Does the file contain the intended combined information?
- Did any unrelated file change?
- After pushing, does the pull request's **Files changed** view match the intended resolution?
