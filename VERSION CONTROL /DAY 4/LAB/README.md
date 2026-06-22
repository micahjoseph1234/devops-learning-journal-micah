# Git Enterprise Lab Assignment
## Banking Loan Management System - End-to-End Git Workflow

---

# Objective

You are a DevOps Engineer supporting a Banking Loan Management Platform.

The application is used for:

- Loan Applications
- Loan Approvals
- Notifications
- Interest Rate Management

Your responsibility is to manage the complete Git lifecycle:

- Repository Creation
- Feature Development
- Branching Strategy
- Rebase
- Merge
- Squash
- Stash
- Revert
- Remote GitHub Integration
- Fetch/Pull
- Push
- Pull Request Workflow

This assignment covers every Git command learned so far.

---

# Architecture

```text
master/main
    |
    ├── feature-loan-application
    |
    ├── feature-loan-approval
    |
    ├── feature-notification
    |
    └── feature-interest-rate
```

---

# Phase 1 - Create Repository

## Objective

Create the Loan Management System repository.

## Tasks

Create repository:

```bash
mkdir loan-management-system

cd loan-management-system

git init
```

Verify:

```bash
git status
git branch
```

---

# Phase 2 - Initial Release

## Objective

Create initial production version.

## Tasks

Create:

```text
README.md
```

Commit:

```text
REL-1 Initial Production Release
```

Verify:

```bash
git log --oneline
```

---

# Phase 3 - Create Feature Branches

## Objective

Multiple teams start development.

## Tasks

Create:

```bash
git branch feature-loan-application

git branch feature-loan-approval
```

Verify:

```bash
git branch
```

Expected:

```text
master

feature-loan-application

feature-loan-approval
```

---

# Phase 4 - Loan Application Feature

## Objective

Develop Loan Application functionality.

## Tasks

Switch:

```bash
git switch feature-loan-application
```

Create:

```text
loan-application.java
```

Create 5 independent commits:

```text
f1cm1 - Created Loan Application Module

f1cm2 - Added Applicant Details

f1cm3 - Added Validation Logic

f1cm4 - Added Eligibility Check

f1cm5 - Added Logging
```

Verify:

```bash
git log --oneline
```

---

# Phase 5 - Rebase Feature Branch

## Objective

Synchronize feature branch with latest master.

## Tasks

Execute:

```bash
git rebase master
```

Questions:

1. Did commit history become linear?
2. Was any merge commit created?

Verify:

```bash
git log --oneline
```

---

# Phase 6 - Merge Feature 1

## Objective

Deploy Loan Application Feature.

## Tasks

Switch:

```bash
git switch master
```

Merge:

```bash
git merge feature-loan-application
```

Verify:

```bash
git log --oneline
```

Questions:

1. Which commits entered master?
2. Was feature history preserved?

---

# Phase 7 - Loan Approval Feature

## Objective

Develop Loan Approval functionality.

## Tasks

Switch:

```bash
git switch feature-loan-approval
```

Create:

```text
loan-approval.java
```

Create commits:

```text
f2cm1 - Created Loan Approval Module

f2cm2 - Added Approval Logic

f2cm3 - Added Rejection Logic

f2cm4 - Added Audit Logging
```

Verify:

```bash
git log --oneline
```

---

# Phase 8 - Rebase Feature 2

## Objective

Update branch using latest production code.

## Tasks

Execute:

```bash
git rebase master
```

Verify:

```bash
git log --oneline
```

Question:

Why should rebase be done before merge?

---

# Phase 9 - Merge Feature 2

## Objective

Deploy Loan Approval Feature.

## Tasks

Switch:

```bash
git switch master
```

Merge:

```bash
git merge feature-loan-approval
```

Verify:

```bash
git log --oneline
```

---

# Phase 10 - Squash Merge

## Objective

Notification Team generated too many commits.

Management wants a clean history.

## Tasks

Create:

```bash
git switch feature-loan-application
```

Create:

```text
notification.java
```

Create:

```text
5 commits
```

Example:

```text
f3cm1
f3cm2
f3cm3
f3cm4
f3cm5
```

Rebase:

```bash
git rebase master
```

Switch:

```bash
git switch master
```

Perform:

```bash
git merge --squash feature-loan-application
```

Verify:

```bash
git status
```

Commit:

```text
REL-2 Notification Module
```

Verify:

```bash
git log --oneline
```

Questions:

1. Did all feature commits appear in master?
2. How many commits entered master?

---

# Phase 11 - Stash Operations

## Objective

Developer receives production incident while coding.

Work must be temporarily saved.

## Tasks

Create:

```bash
git switch -c feature-notification
```

Create:

```text
notification-email.txt
```

Modify several times.

Stage changes.

Verify:

```bash
git status
```

Store work:

```bash
git stash save "notification-email changes"
```

Verify:

```bash
git stash list
```

Create:

```text
sms-notification.txt
```

Stash again.

Create:

```text
push-notification.txt
```

Stash again.

Verify:

```bash
git stash list
```

---

# Phase 12 - Stash Recovery

## Objective

Recover saved work.

## Tasks

Apply latest stash:

```bash
git stash apply
```

Verify:

```bash
git status
```

Drop latest stash:

```bash
git stash drop
```

Verify:

```bash
git stash list
```

Apply specific stash:

```bash
git stash apply stash@{1}
```

Drop specific stash:

```bash
git stash drop stash@{1}
```

Verify:

```bash
git stash list
```

Use:

```bash
git stash pop
```

Verify:

```bash
git stash list
```

Clear everything:

```bash
git stash clear
```

Verify:

```bash
git stash list
```

---

# Phase 13 - Revert Production Defect

## Objective

Production issue found.

Commit:

```text
f2cm3
```

introduced a defect.

## Tasks

Identify commit ID.

Verify:

```bash
git log --oneline
```

Undo:

```bash
git revert <commit-id>
```

Verify:

```bash
git log --oneline
```

Questions:

1. Was commit history preserved?
2. Was a new commit created?

---

# Phase 14 - Remote Repository

## Objective

Integrate with GitHub.

## Tasks

Create GitHub repository:

```text
loan-management-system
```

Connect repository.

Verify:

```bash
git remote -v
```

---

# Phase 15 - Clone Repository

## Objective

Simulate new developer joining team.

## Tasks

Clone repository:

```bash
git clone <repo-url>
```

Verify:

```bash
ls

ls -a

git status

git remote -v
```

Questions:

What gets downloaded during clone?

---

# Phase 16 - Remote Feature Development

## Objective

Developer creates remote feature branch.

## Tasks

Create:

```bash
git switch -c feature-interest-rate
```

Create:

```text
interest-rate.txt
```

Commit:

```text
Added Interest Rate Module
```

Push:

```bash
git push -u origin feature-interest-rate
```

Verify:

```bash
git remote -v
```

Questions:

What does -u mean?

---

# Phase 17 - Fetch vs Pull

## Objective

Synchronize with GitHub.

## Tasks

Verify:

```bash
git status
```

Execute:

```bash
git fetch
```

Questions:

1. Did working directory change?
2. Did local repository update?

Execute:

```bash
git pull
```

Questions:

1. What additional operation occurred?
2. Why is pull considered fetch + merge?

---

# Phase 18 - Remote Management

## Objective

Change repository linkage.

## Tasks

Verify:

```bash
git remote -v
```

Remove:

```bash
git remote remove origin
```

Verify:

```bash
git remote -v
```

Add again:

```bash
git remote add origin <repo-url>
```

Verify:

```bash
git remote -v
```

Add secondary remote:

```bash
git remote add backup <repo-url>
```

Verify:

```bash
git remote -v
```

---

# Final Audit

Provide evidence for:

```bash
git branch

git log --oneline

git show

git stash list

git remote -v

git status
```

---

# Concepts Covered

✅ git init

✅ git add

✅ git commit

✅ git log

✅ git log --oneline

✅ git show

✅ git branch

✅ git switch

✅ git switch -c

✅ git merge

✅ git rebase

✅ git merge --squash

✅ git stash save

✅ git stash list

✅ git stash apply

✅ git stash drop

✅ git stash pop

✅ git stash clear

✅ git revert

✅ git clone

✅ git remote -v

✅ git remote add

✅ git remote remove

✅ git push -u

✅ git fetch

✅ git pull

✅ Feature Branch

✅ Rebase Workflow

✅ Squash Workflow

✅ Stash Workflow

✅ Revert Workflow

✅ Remote Repository Workflow
