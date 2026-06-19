# Git Branching, Merge, Revert & Conflict Resolution Lab

## Objective

Learn and practice:

* git revert
* git branch
* git switch
* git switch -c
* git merge
* Merge Conflict Resolution
* Feature Branch
* Developer Branch
* Integration Branch
* Release Branch

---

# Business Scenario

You are a DevOps Engineer supporting a Banking Loan Management System.

Current Production Release:

```text
REL-1
```

New Features:

```text
Loan Application Module
Loan Approval Module
Loan Notification Module
```

Branching Strategy:

```text
Feature Branch
      ↓
Developer Branch
      ↓
Integration Branch
      ↓
Release Branch
      ↓
Master/Main
```

---

# Task 1 - Create Production Repository

## Objective

Create the initial production release.

## Commands

```bash
mkdir loan-management-system

cd loan-management-system

git init

echo "Customer Registration Module" > customer-registration.java

git add .

git commit -m "REL-1 Initial Production Release"
```

## Verification

```bash
git log --oneline

git branch

git ls-files
```

## Expected Result

```text
master

REL-1 Initial Production Release
```

## Why?

This is the production baseline from which all future branches originate.

---

# Task 2 - Create Loan Application Feature

## Objective

Develop Loan Application functionality independently.

## Commands

```bash
git switch -c feature-loan-application
```

### Commit 1

```bash
echo "Loan Application Module" > loan-application.java

git add .

git commit -m "f1cm1 - Created Loan Application Module"
```

### Commit 2

```bash
echo "Apply Loan Logic" >> loan-application.java

git add .

git commit -m "f1cm2 - Added Loan Application Logic"
```

### Commit 3

```bash
echo "Validation Logic" >> loan-application.java

git add .

git commit -m "f1cm3 - Added Validation Logic"
```

## Verification

```bash
git log --oneline
```

## Expected Result

```text
f1cm3
f1cm2
f1cm1
REL-1
```

## Why?

Feature branches isolate development and prevent unfinished work from affecting production.

---

# Task 3 - Create Loan Approval Feature

## Objective

Develop Loan Approval functionality independently.

## Commands

```bash
git switch master

git switch -c feature-loan-approval
```

### Commit 1

```bash
echo "Loan Approval Module" > loan-approval.java

git add .

git commit -m "f2cm1 - Created Loan Approval Module"
```

### Commit 2

```bash
echo "Approval Logic" >> loan-approval.java

git add .

git commit -m "f2cm2 - Added Loan Approval Logic"
```

### Commit 3

```bash
echo "Rejection Logic" >> loan-approval.java

git add .

git commit -m "f2cm3 - Added Loan Rejection Logic"
```

## Verification

```bash
git log --oneline
```

## Expected Result

```text
f2cm3
f2cm2
f2cm1
REL-1
```

## Why?

Multiple features should evolve independently.

---

# Task 4 - Create Developer Branch

## Objective

Combine all features owned by a single developer.

## Commands

```bash
git switch master

git switch -c developer-micah

git merge feature-loan-application

git merge feature-loan-approval
```

## Verification

```bash
git log --oneline --graph --all
```

## Expected Result

Developer branch contains:

```text
Loan Application
Loan Approval
```

## Why?

Developer Branch validates whether one developer's features work together.

---

# Task 5 - Simulate Another Developer

## Objective

Create independent work for another developer.

## Commands

```bash
git switch master

git switch -c developer-rahul
```

### Commit 1

```bash
echo "Notification Module" > loan-notification.java

git add .

git commit -m "r1cm1 - Created Notification Module"
```

### Commit 2

```bash
echo "Send Notification Logic" >> loan-notification.java

git add .

git commit -m "r1cm2 - Added Notification Logic"
```

## Verification

```bash
git log --oneline
```

## Expected Result

```text
r1cm2
r1cm1
REL-1
```

## Why?

Represents another developer working independently.

---

# Common Mistake (Actual Lab Mistake)

❌ Wrong

```bash
git switch -c developer-rahul
git switch -c integration-team1
git switch -c release-rel2
```

while standing on previous branches.

Result:

```text
developer-micah
      ↓
developer-rahul
      ↓
integration-team1
      ↓
release-rel2
```

All branches point to the same history.

---

✅ Correct

Every logical stage should be created intentionally and merged properly.

---

# Task 6 - Create Integration Branch

## Objective

Combine work from multiple developers.

## Commands

```bash
git switch master

git switch -c integration-team1

git merge developer-micah

git merge developer-rahul
```

## Verification

```bash
git log --oneline --graph --all

git ls-files
```

## Expected Result

```text
Loan Application
Loan Approval
Loan Notification
```

all available together.

## Why?

Integration Branch catches merge issues before release.

---

# Task 7 - Create Release Branch

## Objective

Prepare code for QA testing.

## Commands

```bash
git switch integration-team1

git switch -c release-rel2
```

## Verification

```bash
git branch

git log --oneline
```

## Why?

Release Branch acts as a pre-production environment.

Used for:

* QA Testing
* Regression Testing
* Security Testing
* Performance Testing

---

# Task 8 - Production Rollback Using Revert

## Objective

Rollback a defective feature safely.

## Commands

Find commit:

```bash
git log --oneline
```

Revert:

```bash
git revert <commit-id>
```

Example:

```bash
git revert d53ccaf
```

## Verification

```bash
git log --oneline
```

## Expected Result

```text
Revert "f2cm3 - Added Loan Rejection Logic"
```

appears as a new commit.

## Why?

Revert preserves history and is safe for shared repositories.

---

# Task 9 - Merge Conflict Simulation

## Objective

Create and resolve a merge conflict.

---

## Branch A

```bash
git switch master

git switch -c feature-interest-rate-v1

echo "Interest Rate = 8%" > interest-rate.txt

git add .

git commit -m "Interest Rate 8%"
```

---

## Branch B

```bash
git switch master

git switch -c feature-interest-rate-v2

echo "Interest Rate = 10%" > interest-rate.txt

git add .

git commit -m "Interest Rate 10%"
```

---

## Merge Branch A

```bash
git switch master

git merge feature-interest-rate-v1
```

---

## Merge Branch B

```bash
git merge feature-interest-rate-v2
```

---

## Expected Conflict

```text
<<<<<<< HEAD
Interest Rate = 8%
=======
Interest Rate = 10%
>>>>>>> feature-interest-rate-v2
```

---

## Resolve Conflict

Choose final value:

```text
Interest Rate = 9%
```

Remove:

```text
<<<<<<< HEAD
=======
>>>>>>> feature-interest-rate-v2
```

Save file.

```bash
git add interest-rate.txt

git commit -m "Resolved Interest Rate Conflict"
```

---

## Why Did Conflict Occur?

Both branches modified:

```text
Same File
Same Line
Different Values
```

Git could not decide automatically.

---

# Final Audit

## Branches

```bash
git branch
```

## Commit History

```bash
git log --oneline
```

## Detailed Commit

```bash
git show <commit-id>
```

## Merge Graph

```bash
git log --oneline --graph --all
```

## Files Tracked

```bash
git ls-files
```

---

# Key Interview Notes

## git revert

Creates a new commit that reverses an existing commit.

Recommended in shared repositories.

---

## git merge

Combines changes from one branch into another.

---

## git switch

Moves between existing branches.

---

## git switch -c

Creates and switches to a new branch.

---

## Feature Branch

One feature.

---

## Developer Branch

One developer's work.

---

## Integration Branch

Multiple developers' work.

---

## Release Branch

Final testing area.

---

## Master/Main

Production-ready code only.

---

# Branch Hierarchy

```text
Feature Branch
      ↓
Developer Branch
      ↓
Integration Branch
      ↓
Release Branch
      ↓
Master/Main
```
