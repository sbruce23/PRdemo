# Contributing to PRdemo

PRdemo is deliberately small so that the collaboration mechanics remain visible. A successful contribution changes one line while demonstrating a complete, inspectable workflow.

## Contribution acceptance criteria

A pull request is ready for approval when all of the following are true:

- the head is the contributor's `dev` branch and the base is `sbruce23/PRdemo:main`;
- `fav_animal.txt` contains exactly one intentional new animal line;
- the pull request contains no credentials, private data, grades, or unrelated files;
- the commit message describes the change in the imperative voice;
- the pull-request description explains the purpose and the verification performed;
- the contributor has responded to review questions or requested changes; and
- GitHub reports that the pull request can be merged, or any conflict has been intentionally resolved and re-verified.

## Responsibilities by role

### Contributor

The contributor owns the change. They synchronize before branching, inspect working and staged diffs, make focused commits, push to their fork, open the pull request in the correct direction, and explain their decisions during review.

### Reviewer

The reviewer reads the pull-request description and **Files changed**, checks the acceptance criteria, asks specific questions, and chooses **Comment**, **Approve**, or **Request changes**. A reviewer should not approve merely because the change is small.

### Maintainer

The maintainer decides whether the contribution is ready to become part of the original repository. The maintainer may request additional evidence and performs the merge in GitHub. Approval and merge are related but distinct actions.

## Review prompts

Use at least two of these prompts when discussing a pull request:

1. Which repository and branch are the head? Which are the base?
2. What does the diff prove changed? What does it prove did not change?
3. Did the contributor stage a named file or a broad directory?
4. Does the commit message describe the recorded snapshot?
5. If a new commit is pushed to `dev`, what happens to the existing pull request?
6. If GitHub reports a conflict, what should the final file contain?

## Public-repository boundary

This repository is public and retained as a practice sandbox. Do not use it for graded submissions or material that reveals student records or confidential data. Follow the instructor's separate directions for private course work.
