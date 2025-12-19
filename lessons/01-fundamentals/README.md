# 01 — Fundamentals: Commits, working tree, and staging area

## What is Git?

Git is a tool (version control system) that helps you:
A version control system (VCS) is software that helps developers to record chnages to files over time in a scpecial database called repository. It allows you to
save and manage different versions of your files and code.
work with others, keep track of changes, and undo mistakes.

So we can lookup the history and see who has made changes when and why.
And we can easily revert to previous versions if something goes wrong.

- Track changes to files over time (Track History & Work together)

we have two types of version control systems:

- **Centralized** VCS (CVCS): A single server stores all the versioned files, and clients check out files from that central place.
  - Subversion (SVN)
  - Team Foundation Server (TFS)
- **Distributed** VCS (DVCS): Clients fully mirror the repository, including its full history.
- Git
- Mercurial

Git is the most popular DVCS today: - Free - Open Source - Super fast - Scalable - Powerful branching and merging

## Prerequisites

Git installed and configured (`git --version`)

[Instllation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

You can download Git for free from [git-scm.com](https://git-scm.com/downloads).

How to use Git:

- Command line (Git Bash, Terminal, PowerShell)
- GUI tools (GitHub Desktop, Sourcetree, GitKraken)
- IDE integrations (VS Code, IntelliJ, etc.)

## Check your Git installation

Open your terminal or command prompt and run:

```bash
git --version
```

## How to Configure Git

Setting name, email, and default editor and line endings
in can be done at

- System level (All users)
- Global level (All repositories for current user)
- Local level (Current repository)

> [!NOTE]
> git config --[config level] [keyName] "[keyValue]"

> [!NOTE]
> We need double quotes for values with spaces

```bash

git config --global user.name "Your Name"
git config --global user.email you@example.com
git config --global core.editor "code --wait"   # setting default editor for VS Code

# we need to set end of line handling based on OS(windows: \r\n, mac/linus: \n)

git config --global core.autocrlf true   # for Windows
git config --global core.autocrlf input  # for Mac/Linux

# for checking the configuration
git config --list

# for editing the configuration file in default editor
git config --global --edit
```

## Steps

### Initialize a disposable repo and create a file

for creating a directory & moving inside the directory using commands:

```bash
mkdir git-fundamentals && cd git-fundamentals
```

For Initializing the directory with git:

```bash
git init
```

> [!NOTE]
> git init command result is ` Initialized empty Git repository in path/git-fundamnetals/.git/`

Other usefull commands to check the directory:

```bash
# to list the files
ls

# to list the files include hiddens
ls -a
```

### Stage and commit

Git stores complete snapshots of your project (conceptually: the content of files at a moment), and each commit points to a snapshot plus some metadata (author, message, parent commit(s)). Internally it’s clever and de-duplicates identical content, but the model you should use is: commit = snapshot.

> [!NOTE]
> Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

> [!NOTE]
> Committed means that the data is safely stored in your local database

```bash
git add hello.txt
git commit -m "Add hello.txt"
git log --oneline --graph --decorate
```

### Edit, stage partially, and observe index

```bash
echo "Line 2" >> hello.txt # linuxs command to change file
git add -p hello.txt    # try staging a hunk interactively
git commit -m "Update hello.txt (partial)"
```

> [!NOTE]
> By just running `git commit` you can use commit templated opend in default editor

### Inspect the working tree vs HEAD

It shows you exactly what changed, line by line, without changing anything.

> [!Note]
> git diff compares working directory ↔ staging area

```bash
git diff             # changes in working tree not staged
git diff --staged    # staged changes compared to HEAD
```

In plain terms, `git status` answers three questions at once:

- What branch am I on?
- What files have changed?
- What will happen if I commit right now?

```bash
git status
```

Where git status tells you that something changed, git diff tells you how.

## Expected outcome

- A small commit history showing initial add and update commits.
- Familiarity with `git status`, `git add`, `git commit`, `git diff`, and `git log`.

## Notes and recovery

- If you accidentally staged unwanted changes: `git reset <file>` to unstage.
- To discard working tree changes: `git restore <file>` or `git checkout -- <file>` (older Git versions).

## Commiting code best practices

Below is a compact set of best practices that actually scale—from solo projects to large monorepos.

### Atomic and purposeful

One commit should do one logical thing.

- Good:
  - “Fix null handling in user resolver”
  - “Extract auth guard into shared lib”
- Bad:
  - “Fix stuff”
  - “WIP”
  - “Changes”

If you need “and”, you probably need another commit

### Commit what you intend, not what you touched

### Choosing the right commit type

Use these consistently:

- `feat`: new user-visible behavior
- `fix`: bug fix
- `refactor`: code change with no behavior change
- `test`: add or adjust tests
- `docs`: documentation only
- `chore`: tooling, configs, dependencies
- `perf`: performance improvement
- `ci`: CI/CD changes
- `build`: build system changes

Never do these:

- Committing generated files (unless required)
- Mixing refactor + behavior change
- “WIP” on main branches
- Massive “cleanup” commits with no explanation
- Fixing formatting and logic in the same commit

Run this mentally:

- Does this commit do one thing?
- Would I revert this commit alone if needed?
- Does the summary make sense without context?
- Do tests pass?
- Would a teammate thank me for this message?
