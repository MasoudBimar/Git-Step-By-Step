# Git Step By Step

[![Lessons](https://img.shields.io/badge/lessons-1-brightgreen)](LESSONS.md) [![Contribute](https://img.shields.io/badge/contribute-welcome-blue)](https://github.com/issues) [![License](https://img.shields.io/badge/license-check-lightgrey)](LICENSE)

A practical, hands-on learning guide to Git — one concept at a time.

This repository is a learning log and collection of short, focused experiments that teach how Git models history and how common workflows behave in real situations. Each lesson emphasizes understanding and recovery strategies, not rote memorization of commands.

## Table of Contents

- **Getting Started** — purpose and audience
- **Snapshots** — what you'll learn
- **History** — suggested workflow
- **Branching** — ordered topics and exercises
- **Collaboration** — practical scenarios and solutions
- **Rewriting History** — how to add lessons or corrections
- **License** — repository license

## About

This repository now includes a lessons in `lessons/`. Each lesson is a self-contained folder with a `README.md` explaining the objective, steps, expected outcomes, and recovery notes.

This repository is for learners who want to move beyond using Git and toward truly understanding it. Lessons are intentionally short, reproducible, and designed for experimentation in disposable repositories.

Who this is for:

- New developers learning version control
- Developers who use Git but want stronger mental models
- Educators looking for compact, example-driven exercises

What this is not:

- A complete Git reference
- A replacement for official docs

## Goals

- Build an intuitive model of commits, branches, and history
- Learn safe workflows for feature development and collaboration
- Practice recovery: undoing mistakes, resolving conflicts, and rewriting history
- Gain confidence with merge, rebase, cherry-pick, and tagging

## How to use this repo

1. Clone this repository locally.
2. Work in disposable test repositories for each lesson (use `git init` or clones).
3. Follow the step-by-step exercises in each lesson folder and run commands yourself.
4. Break things intentionally and practice recovery strategies shown in the examples.

Suggested quick start:

```bash
git clone https://github.com/MasoudBimar/Git-Step-By-Step.git
cd Git-Step-By-Step
# open a lesson folder and follow the README there
```

## Learning path (recommended order)

1. [Fundamentals](lessons/01-fundamentals/README.md): commits, working tree, staging area
2. [History](lessons/02-history/README.md): viewing logs, reflog, and commit anatomy
3. [Branching](lessons/03-branching/README.md): creating, switching, and merging branches
4. [Collaboration](lessons/04-collaboration/README.md): remotes, fetch, pull, push
5. [Rewriting History](lessons/05-rewriting-history/README.md): interactive rebase, amend, and squash
6. [Conflict Resolution](lessons/06-conflict-resolution/README.md): detect, resolve, and verify
7. Advanced workflows: trunk-based, feature branches, forking
8. Recovering from mistakes: reset, revert, reflog strategies

Each numbered lesson contains small exercises and example commands. Look in the repository root for lesson folders or search by topic.

## Git Command cheat sheet

1. [Snapshots](lessons/00-cheat-sheets/1.creating-snapshots.md)
2. [Viewing History](lessons/00-cheat-sheets/2.viewing-history-and-diff.md)
3. [Browsing History](lessons/00-cheat-sheets/3.browsing-history.md)
4. [Branching & Merging](lessons/00-cheat-sheets/4.branching-merging.md)
5. [Collaboration](lessons/00-cheat-sheets/5.collaboration.md)
6. [Rewriting History](lessons/00-cheat-sheets/6.rewriting-history.md)

## Examples

- Rebase vs Merge: small reproducible repo demonstrating both
- Undoing commits safely: using `git revert` and `git reset`
- Resolving merge conflicts with practical examples

## Contributing

- Suggest a lesson or improvement via issues or pull requests.
- Add reproducible examples and short explanations (keep lessons focused).
- Use clear commit messages and include the lesson folder path in your PR.

## License

This project is licensed under the terms in the `MIT LICENSE` file.

---
