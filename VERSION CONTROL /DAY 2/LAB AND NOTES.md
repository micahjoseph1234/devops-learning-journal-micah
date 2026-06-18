# Day 11 Git Misc Commands Lab - Banking ETL Release Management

## Objective

You are a DevOps Engineer supporting a Banking ETL (Extract → Transform → Load) application.

The ETL team has asked you to manage source code versions, investigate changes, exclude build artifacts, recover from mistakes, and maintain release history using Git.

You must complete the tasks using Git CLI commands only.

---

# Scenario

A new ETL application named:

```text
banking-etl
```

is being developed.

The repository will contain:

* ETL extraction scripts
* Data transformation logic
* Documentation
* Build artifacts
* Temporary files

As the DevOps Engineer, your responsibility is to ensure only valid source code is tracked and released.

---

# Task 1 - Repository Initialization

Create a new repository named:

```text
banking-etl
```

Requirements:

* Initialize Git repository
* Verify repository creation
* Verify Git metadata exists
* Configure Git username and email

---

# Task 2 - Initial Security Setup

Before any code is committed, management wants Git ignore rules configured.

Create a `.gitignore` file.

The following must never be tracked:

```text
*.jar
*.war
target/
build/
credentials.json
secrets.json
```

Requirements:

* Create ignore rules
* Make `.gitignore` the first commit in repository history
* Verify commit history

---

# Task 3 - ETL Source Creation

Create the following files:

```text
extract.java
transform.java
load.java

README.md

etl-design.doc
```

Add sample content to every file.

Requirements:

* Verify repository status
* Verify tracked files
* Verify untracked files

---

# Task 4 - Selective Staging

The Release Manager approves only:

```text
extract.java
transform.java
README.md
```

for the first release.

Requirements:

* Stage only approved files
* Do NOT stage remaining files
* Verify staging status

---

# Task 5 - Staging Mistake Recovery

A junior developer accidentally stages:

```text
etl-design.doc
```

Requirements:

* Remove it from staging area
* Ensure file still exists locally
* Verify repository status

---

# Task 6 - Permanent File Removal

Management decides:

```text
load.java
```

must be deleted completely.

Requirements:

* Remove it from Git staging
* Remove it from working directory
* Verify file removal

---

# Task 7 - First Release

Create Release 1.

Requirements:

* Create commit using enterprise-style commit message
* View complete commit history
* View compact commit history
* Verify tracked files

Example release naming conventions:

```text
REL-1001
CR-1001
REL-JUNE
```

Use your own release naming convention.

---

# Task 8 - Incremental Development

Modify:

```text
extract.java
```

multiple times.

Create at least three separate commits representing:

```text
Enhancement 1
Enhancement 2
Enhancement 3
```

Requirements:

* Commit each change independently
* Maintain meaningful commit messages

---

# Task 9 - History Investigation

The Production Support Team reports an issue in:

```text
extract.java
```

Requirements:

Find:

1. Complete repository history
2. Last 3 commits
3. Compact commit history
4. History related only to extract.java

Document the commands used.

---

# Task 10 - Commit Investigation

The Support Team provides a commit ID.

Requirements:

* View complete details of a specific commit
* Identify:

  * Author
  * Commit message
  * File changes
  * Timestamp

Document the command used.

---

# Task 11 - Difference Analysis

Modify:

```text
extract.java
```

but do NOT commit immediately.

Requirements:

* Compare current file against last committed version
* Identify exact changes
* Verify observations

Document command used.

---

# Task 12 - Soft Reset Scenario

A release was committed using an incorrect commit message.

Requirements:

* Undo the latest commit
* Preserve staged changes
* Recreate commit with a corrected message

Verify status before and after operation.

---

# Task 13 - Mixed Reset Scenario

A release was committed too early.

Requirements:

* Undo latest commit
* Return changes to working directory
* Continue editing files

Verify status before and after operation.

---

# Task 14 - Hard Reset Scenario

A failed ETL experiment introduced unwanted changes.

Management wants repository restored to a previous stable commit.

Requirements:

* Identify stable commit
* Reset repository to that commit
* Verify:

  * Commit history
  * Tracked files
  * Working directory contents

Document observations.

---

# Task 15 - Final Audit

Provide evidence for:

1. Current repository status
2. Current tracked files
3. Current commit history
4. Current HEAD commit
5. Files ignored by Git
6. Stable release currently available

---

# Deliverables

Submit:

## Commands Executed

Paste all commands executed.

---

## Screenshots

Include screenshots for:

```text
git status
git log
git log --oneline
git ls-files
git diff
git show
```

---

## Concept Questions

1. Difference between git add and git commit.
2. Difference between git rm --cached and git rm -f.
3. Difference between git log and git show.
4. Purpose of git diff.
5. Why should .gitignore be the first commit?
6. Difference between soft, mixed and hard reset.
7. Why is git reset discouraged in shared repositories?
8. Explain how Git tracks files.
9. What is HEAD?
10. What happens to Working Directory, Staging Area and Repository during each reset type?
