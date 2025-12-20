# Snapshots and the Staging Area

## Untracked files

An untracked file is any file in your project folder that Git is not yet tracking.

These are files you've created or copied into the folder, but haven't told Git to watch.

## Workspace vs Staging Area (Index)

### Workspace (Working directory)

- The actual files on your disk (what VS Code edits).
- When you **create / edit / rename / delete** a file, that happens here first.

### Staging area (Index)

- A "shopping cart" of changes you **intend** to include in the next commit.
- It holds a snapshot of selected changes, independent of what you keep editing in the workspace.

### Repository (HEAD)

- The last committed snapshot (history).

So Git is basically tracking **three versions** of things:

1. last commit (HEAD)
2. staged snapshot (index)
3. current files (workspace)

---

## Why we need `git add`

`git add` means: **"Put this change into the next commit."**

It's not only for "adding new files". It stages **any kind of change**:

- new file
- modified content
- deletion
- rename/move (staged as delete+add, then Git may detect it as rename)

### Why Git doesn't auto-stage every change

Because that would make commits messy and risky:

- You often make multiple experiments, half-finished edits, or temporary changes.
- Staging lets you **choose** what belongs together logically in one commit (clean history).
- You can stage **part** of a file (hunks/lines) and leave the rest for later.

So: **every change happens in the workspace**, but only changes you `git add` are included in the next commit.

---

## How Git treats different kinds of file changes

### 1) New files

- You create a file -> it's **untracked** (Git knows it exists but doesn't track its content yet).
- `git status` shows: **Untracked files**
- After `git add <file>` -> it becomes **staged as a new file**
- After `git commit` -> it becomes **tracked**

**Key idea:** Git won't include new files in commits unless you explicitly `git add` them.

---

### 2) Modified files (content changes)

- You edit a tracked file -> `git status` shows it as **modified** (unstaged).
- Run `git add <file>` -> the _current version_ of that file is copied into the **staging area**.
- If you edit again after staging:

  - you now have **staged changes** + **unstaged changes** at the same time.

**Key idea:** staging is a snapshot, not a live link.

---

### 3) Deleted files

- You delete a tracked file in VS Code -> workspace removes it.
- `git status` shows: **deleted** (unstaged).
- To include the deletion in the next commit, you must stage it:

  - `git add -u` (stages deletions + modifications of tracked files)
  - or `git rm <file>` (does the delete + stage in one step)

**Key idea:** deletion must be staged too, otherwise the commit won't record it.

---

### 4) Renamed / moved files

Git doesn't store "rename" as a special operation in history.
Instead, it records:

- **one file deleted**
- **another file added**
  Then it _detects_ it as a rename when similarity is high enough.

Practically:

- rename/move in VS Code -> shows as delete+add (or "renamed" depending on tooling)
- stage it (`git add -A` is common) -> commit it
- Git likely displays it as a rename in logs/diffs

**Key idea:** rename is "detected", not "stored".

---

## What to run every time something changes (practical rules)

You **don't** need to run `git add` after every tiny change. You run it when you want to **prepare a commit**.

Useful commands:

- `git add <file>` -> stage specific file
- `git add -A` -> stage **everything** (new, modified, deleted)
- `git add -u` -> stage **tracked** files only (modified + deleted, no new files)

Typical workflow:

1. edit freely (workspace)
2. stage logical chunk(s) (`git add ...`)
3. commit one coherent change (`git commit -m "..."`)

---

## A tiny cheat sheet (status -> action)

- **Untracked** (new file) -> `git add <file>` or `git add -A`
- **Modified** (content) -> `git add <file>` (or stage hunks in VS Code)
- **Deleted** (tracked) -> `git add -u` or `git rm <file>`
- **Renamed/moved** -> usually `git add -A` and commit

---

## The 3-tree mental model (the whole trick)

Think of Git as tracking **three snapshots**:

```
(Repository)        (Staging Area / Index)        (Workspace)
   HEAD   <------->       INDEX        <------->     FILES
 last commit           next commit draft            your disk
```

- **Workspace** = what you edit in VS Code.
- **Index (staging)** = what you _plan_ to commit next.
- **HEAD** = what you _already_ committed.

### The core commands

- `git add` : **Workspace -> Index**
- `git commit` : **Index -> HEAD**
- `git restore <file>` : **Index/HEAD -> Workspace** (depending on flags)
- `git restore --staged <file>` : **Index -> (match) HEAD** (unstage)

---

## Why staging exists (why Git doesn't auto-stage everything)

Staging lets you:

- make **small, coherent commits** (clean history, easy review)
- stage **only parts of a file** (hunks/lines)
- keep experimenting in the workspace without polluting the next commit

If Git auto-staged everything, every commit would include your "oops" edits, debug prints, and half-finished work. Staging is your "commit firewall".

---

## What `git status` is really telling you

Git compares:

- **Workspace vs Index** -> "Changes not staged for commit"
- **Index vs HEAD** -> "Changes to be committed"
- also shows **Untracked files** (not in HEAD or Index)

---

## Examples for each file type of change

### 1) New file (untracked -> staged -> committed)

**You do:**

```bash
echo hi > a.txt
git status
```

**You see:**

```
Untracked files:
  a.txt
```

**Stage it:**

```bash
git add a.txt
git status
```

**Now:**

```
Changes to be committed:
  new file: a.txt
```

**Commit:**

```bash
git commit -m "Add a.txt"
```

---

### 2) Modified file (content change)

Edit `app.ts`.

**After edit:**

```
Changes not staged for commit:
  modified: app.ts
```

**Stage it:**

```bash
git add app.ts
```

**Now:**

```
Changes to be committed:
  modified: app.ts
```

**Important: staged is a snapshot**
If you edit `app.ts` again _after_ staging:

```
Changes to be committed:
  modified: app.ts

Changes not staged for commit:
  modified: app.ts
```

That means: "some changes staged, more changes still only in workspace".

---

### 3) Deleted file

Delete tracked `old.txt`.

**After delete:**

```
Changes not staged for commit:
  deleted: old.txt
```

**Stage deletion:**

```bash
git add -u
# or: git rm old.txt   (delete + stage)
```

**Now:**

```
Changes to be committed:
  deleted: old.txt
```

---

### 4) Renamed / moved file

Rename `a.txt` -> `b.txt`.

**Git internally records:** delete `a.txt` + add `b.txt`
Then it often **detects** it as a rename.

Stage all:

```bash
git add -A
```

You might see:

```
Changes to be committed:
  renamed: a.txt -> b.txt
```

(or as delete+new, depending on tooling). Either way, commit works.

---

## The "which add command should I use?" cheat sheet

- Stage **everything** (new + modified + deleted):

  ```bash
  git add -A
  ```

- Stage **only tracked files** (modified + deleted, NOT new):

  ```bash
  git add -u
  ```

- Stage **specific file**:

  ```bash
  git add path/to/file
  ```

---

## Micro diagram for `git status` sections

```
HEAD  <- compare ->  INDEX  <- compare ->  WORKSPACE
        (staged)                (unstaged)
```

- "Changes to be committed" = INDEX differs from HEAD
- "Changes not staged..." = WORKSPACE differs from INDEX
- "Untracked" = only in WORKSPACE

---

## One practical workflow (clean commits)

1. Edit freely
2. `git status`
3. `git add -p` (stage hunks) or stage in VS Code
4. `git diff --staged` (review what you're about to commit)
5. `git commit -m "Meaningful message"`

Staging is basically "pre-commit review".

If you use VS Code's Source Control panel, it's the same model: "Changes" = workspace, "Staged Changes" = index.
