# PRdemo: practice contributing through a pull request

This public repository is a small, low-stakes environment for practicing the STAT 315 collaborative workflow:

1. fork the original repository on GitHub;
2. clone your fork to your computer;
3. identify the original repository as `upstream`;
4. synchronize `main` and create a `dev` branch;
5. make, inspect, stage, and commit one focused change;
6. push `dev` to your fork;
7. open a pull request from your fork's `dev` branch to this repository's `main` branch;
8. participate in review, revision, and merge; and
9. synchronize your copies after the pull request is merged.

> **Public-practice warning:** forks, commits, usernames, and pull-request discussions in this repository are public. Do not include grades, private data, credentials, or confidential project material. Required STAT 315 work belongs in the private course environment specified by the instructor.

## The repository topology

During this exercise, three repositories are involved:

| Repository | Git remote name | Purpose |
|---|---|---|
| `https://github.com/sbruce23/PRdemo` | `upstream` | The original repository. You request changes here through a pull request. |
| the `PRdemo` repository owned by the account returned by `gh api user --jq .login` | `origin` | Your GitHub fork. You may push your `dev` branch here. |
| `~/stat315/PRdemo` | none; this is local | Your working copy on your computer. Git commands operate here. |

`origin` and `upstream` are conventional local nicknames. Confirm what they mean in your clone with `git remote -v`; never rely on memory.

## Before you begin

Install Git and the GitHub CLI, authenticate once, and set your commit identity:

```bash
git --version
gh --version
gh auth status
GITHUB_USER=$(gh api user --jq .login)
git config --global user.name "$(gh api user --jq '.name // .login')"
git config --global user.email "${GITHUB_USER}@users.noreply.github.com"
```

These commands use the authenticated account's display name and GitHub-provided no-reply address. Never place a password or access token in a command, file, slide, or commit.

## Step 1: fork the original repository on GitHub

Open <https://github.com/sbruce23/PRdemo>, select **Fork**, keep the repository name `PRdemo`, and create the fork under your own GitHub account.

**Verify:** GitHub should identify the new repository as a fork of `sbruce23/PRdemo`. In the terminal, `gh api user --jq .login` prints the owner name that should appear in the page heading.

## Step 2: clone your fork and identify the original repository

The first command obtains the login for the account authenticated in GitHub CLI, so no placeholder username is needed.

```bash
mkdir -p ~/stat315
cd ~/stat315
GITHUB_USER=$(gh api user --jq .login)
git clone "https://github.com/${GITHUB_USER}/PRdemo.git"
cd PRdemo
git remote add upstream https://github.com/sbruce23/PRdemo.git
git remote -v
```

**Verify:** the output should show `origin` pointing to your fork and `upstream` pointing to `sbruce23/PRdemo` for fetch and push.

## Step 3: synchronize `main`, then create `dev`

```bash
git switch main
git fetch upstream
git merge --ff-only upstream/main
git push origin main
git switch -c dev
git status
```

`git fetch upstream` downloads upstream information without changing your files. `git merge --ff-only upstream/main` advances local `main` only when Git can do so without creating a new merge commit. `git switch -c dev` creates and checks out the course development branch.

**Verify:** `git status` should report `On branch dev` and a clean working tree.

## Step 4: make one focused change

Open `fav_animal.txt` and add exactly one animal on a new final line. For example, Scott might add:

```text
Red panda
```

Inspect the change before staging it:

```bash
git status --short
git diff -- fav_animal.txt
```

**Verify:** the diff should show one intentional added line and no unrelated edits.

## Step 5: stage and commit the exact change

```bash
git add fav_animal.txt
git diff --staged -- fav_animal.txt
git commit -m "Add red panda to favorite animals"
git status
git show --stat --oneline HEAD
```

`git add fav_animal.txt` stages only the named file. Avoid `git add .` in this exercise because it can stage unrelated files. A commit records the staged snapshot in your local repository; it does not change either GitHub repository.

**Verify:** the staged diff contains only your line, and the final status is clean.

## Step 6: publish `dev` to your fork

```bash
git push -u origin dev
git branch -vv
```

The push changes your fork (`origin`). It does not change the original repository (`upstream`). The `-u` option records the tracking relationship so later pushes from `dev` can use `git push`.

## Step 7: open the pull request from the command line

```bash
gh pr create \
  --repo sbruce23/PRdemo \
  --base main \
  --head "$(gh api user --jq .login):dev" \
  --title "Add red panda to favorite animals" \
  --body "Adds Red panda to fav_animal.txt. I inspected the working and staged diffs before committing."
```

The pull-request direction is:

```text
account returned by gh api:dev  --->  sbruce23:main
             head                         base
```

**Verify:** `gh pr view --web` opens the pull request, and the GitHub page shows the intended head and base.

## Step 8: review, revise, and merge

On GitHub, reviewers inspect **Files changed** and may comment, approve, or request changes. Approval is a review judgment; merging is a separate maintainer action.

If a reviewer asks for a revision, remain on the same `dev` branch, make a new focused commit, and push again:

```bash
git switch dev
git status
# edit the requested file
git diff
git add fav_animal.txt
git diff --staged
git commit -m "Address pull request feedback"
git push
```

The existing pull request updates automatically. Do not open a second pull request for the same contribution.

The maintainer reviews the final changes and uses the GitHub interface to merge an acceptable pull request. See [CONTRIBUTING.md](CONTRIBUTING.md) for the acceptance criteria and review responsibilities.

## Step 9: synchronize after merge

After GitHub reports that the pull request was merged:

```bash
git switch main
git fetch upstream
git merge --ff-only upstream/main
git push origin main
git branch -d dev
```

Deleting the local `dev` branch is safe only after its work has been merged. Deleting the remote branch in GitHub is optional for this practice exercise.

## Merge conflicts

A merge conflict means Git cannot infer the intended combined content. First decide what the final file should say; then edit the file to that result, validate it, stage it, and commit it. Use GitHub's conflict editor only for a small text conflict that you fully understand. For a multi-file, code, or test-sensitive conflict, resolve locally and run the relevant checks. The complete procedure and abort path are in [docs/conflicts.md](docs/conflicts.md).

## Troubleshooting

- **`remote upstream already exists`:** run `git remote -v`; if the URL is wrong, use `git remote set-url upstream https://github.com/sbruce23/PRdemo.git`.
- **`dev` already exists:** use `git switch dev`; do not create it again.
- **Push rejected:** confirm that `origin` is your fork and that you are authenticated with the account that owns it.
- **Pull request has the wrong direction:** close it without merging and recreate it with the authenticated account's `dev` branch as head and `sbruce23:main` as base.
- **Working tree is not clean before synchronization:** commit the intended work or use `git stash` only if you understand how to restore it.
- **You are unsure what a command changed:** stop and run `git status`, `git diff`, `git diff --staged`, `git branch -vv`, and `git remote -v` before taking another action.

## Learning objective

Success is not merely opening a pull request. You should be able to explain which repository and branch each command changed, why the pull request has a particular head and base, what evidence a reviewer should inspect, who has merge authority, and how all copies become synchronized after merge.
