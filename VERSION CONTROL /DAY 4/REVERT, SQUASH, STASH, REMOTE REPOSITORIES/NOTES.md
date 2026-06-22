# Git Advanced Concepts Notes

## Git Revert

### Purpose

Used to safely undo a commit by creating a new commit that reverses the changes introduced by the selected commit.

### Syntax

```bash
git revert <commit-id>
```

### Example

```bash
git log --oneline

git revert d53ccaf
```

### What Happens?

Before:

```text
cm1
cm2
cm3
```

After Revert:

```text
Revert "cm3"
cm3
cm2
cm1
```

### Key Points

* Creates a new commit.
* Preserves commit history.
* Recommended for shared repositories.
* Does not delete existing commits.

### Real-World Scenario

A production release introduces a bug.

Instead of rewriting history using reset, use revert to safely roll back the problematic change.

### Interview Question

**Why is git revert preferred over git reset in shared repositories?**

Because revert preserves commit history and does not rewrite commits that other developers may already have.

---

# Git Rebase

### Purpose

Used to synchronize a feature branch with the latest target branch while maintaining a clean and linear commit history.

### Syntax

```bash
git rebase master
```

### Example

Before Rebase:

```text
master

cm1
cm2
cm3


feature

f1
f2
f3
```

Command:

```bash
git switch feature

git rebase master
```

After Rebase:

```text
cm1
cm2
cm3
f1
f2
f3
```

### What Happens Internally?

Git:

1. Temporarily removes feature commits.
2. Moves branch to latest master.
3. Replays feature commits on top of master.

### Benefits

* Linear commit history.
* Easier debugging.
* Reduces merge conflicts.
* Cleaner pull requests.

### Best Practice

Always rebase feature branches before merging.

### Warning

Avoid rebasing shared branches such as:

```text
main
develop
integration
release
```

because rebase rewrites commit history.

### Interview Question

**Difference between Merge and Rebase?**

Merge combines histories and creates a merge commit.

Rebase rewrites history and replays commits on top of another branch.

---

# Git Squash

### Purpose

Used to combine multiple commits into a single commit.

### Syntax

```bash
git merge --squash feature1

git commit -m "Combined changes"
```

### Example

Feature Branch:

```text
f1
f2
f3
f4
f5
```

Normal Merge:

```text
master

f1
f2
f3
f4
f5
```

Squash Merge:

```text
master

CR-1001 Loan Application Feature
```

### Benefits

* Cleaner history.
* Easier auditing.
* Better pull request readability.
* Removes unnecessary intermediate commits.

### Real-World Scenario

A feature branch contains 200 development commits.

Management only wants a single business-level commit in production history.

### Interview Question

**Does git merge --squash create a merge commit?**

No.

It stages combined changes and requires a manual commit afterwards.

---

# Git Stash

### Purpose

Temporarily stores uncommitted changes so that developers can switch tasks or branches without committing incomplete work.

### Save Changes

```bash
git stash save "work in progress"
```

### View Stashes

```bash
git stash list
```

Example:

```text
stash@{0}: Loan Approval Work
stash@{1}: Notification Changes
```

### Restore Latest Stash

```bash
git stash apply
```

### Restore Specific Stash

```bash
git stash apply stash@{2}
```

### Restore and Delete

```bash
git stash pop
```

### Delete Latest Stash

```bash
git stash drop
```

### Delete Specific Stash

```bash
git stash drop stash@{2}
```

### Delete All Stashes

```bash
git stash clear
```

### Apply vs Pop

| Command         | Restores Changes | Removes Stash |
| --------------- | ---------------- | ------------- |
| git stash apply | Yes              | No            |
| git stash pop   | Yes              | Yes           |

### Real-World Scenario

A production incident occurs while working on a feature.

Stash current work, switch branches, fix production, then restore unfinished work later.

### Interview Question

**What is the difference between stash apply and stash pop?**

Apply restores changes but keeps the stash entry.

Pop restores changes and removes the stash entry.

---

# Working with Remote Repositories (GitHub)

## Purpose

Enable collaboration between multiple developers through a central GitHub repository.

### Architecture

```text
Working Directory
        ↓
Staging Area
        ↓
Local Repository
        ↓
Remote Repository (GitHub)
```

---

## Clone Repository

Used to copy an entire remote repository locally.

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/company/project.git
```

### Downloads

* Source code
* Commit history
* Branches
* Tags
* Git metadata

---

## View Remote Repositories

```bash
git remote -v
```

Example:

```text
origin https://github.com/company/project.git (fetch)

origin https://github.com/company/project.git (push)
```

---

## Add Remote Repository

```bash
git remote add origin <repository-url>
```

---

## Remove Remote Repository

```bash
git remote remove origin
```

---

## Push Changes

```bash
git push -u origin feature1
```

### Meaning

```text
Local Branch
      ↓
Remote Branch
```

### Why Use -u?

Sets upstream tracking.

Future pushes can be done using:

```bash
git push
```

---

## Fetch

```bash
git fetch
```

### What It Does

Downloads changes from GitHub and updates the local repository.

### What It Does Not Do

Does not update the working directory.

### Flow

```text
GitHub
   ↓
Local Repository
```

---

## Pull

```bash
git pull
```

### Equivalent To

```text
git fetch + git merge
```

### Flow

```text
GitHub
   ↓
Local Repository
   ↓
Working Directory
```

---

## Pull Request (PR)

### Workflow

```text
Feature Branch
      ↓
Push
      ↓
Pull Request
      ↓
Code Review
      ↓
Approval
      ↓
Merge
```

### Purpose

* Code review
* Collaboration
* Quality checks
* Approval before merge

---

# Quick Comparison Table

| Command            | Purpose                           |
| ------------------ | --------------------------------- |
| git revert         | Safely undo a commit              |
| git rebase         | Replay commits on latest branch   |
| git merge --squash | Combine multiple commits into one |
| git stash          | Temporarily save uncommitted work |
| git clone          | Copy remote repository            |
| git push           | Upload commits to GitHub          |
| git fetch          | Download changes only             |
| git pull           | Download and merge changes        |
| Pull Request       | Request code review before merge  |

```
```
