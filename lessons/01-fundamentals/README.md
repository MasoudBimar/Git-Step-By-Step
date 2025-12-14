# 01 — Fundamentals: Commits, working tree, and staging area

Difficulty: Beginner

Estimated time: 15–25 minutes

## Objective

Understand the difference between the working tree, the staging area (index), and commits.

## Prerequisites

- Git installed and configured (`git --version`)

## Steps

1. Initialize a disposable repo and create a file

```bash
mkdir git-fundamentals && cd git-fundamentals
git init
echo "Hello" > hello.txt
git status
```

2. Stage and commit

```bash
git add hello.txt
git commit -m "Add hello.txt"
git log --oneline --graph --decorate
```

3. Edit, stage partially, and observe index

```bash
echo "Line 2" >> hello.txt
git add -p hello.txt    # try staging a hunk interactively
git commit -m "Update hello.txt (partial)"
```

4. Inspect the working tree vs HEAD

```bash
git diff             # changes in working tree not staged
git diff --staged    # staged changes compared to HEAD
```

## Expected outcome

- A small commit history showing initial add and update commits.
- Familiarity with `git status`, `git add`, `git commit`, `git diff`, and `git log`.

## Notes and recovery

- If you accidentally staged unwanted changes: `git reset <file>` to unstage.
- To discard working tree changes: `git restore <file>` or `git checkout -- <file>` (older Git versions).

## Files

- `hello.txt` — example file used for exercises.
