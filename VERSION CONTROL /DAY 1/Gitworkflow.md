# Day 1 - Git & GitHub Fundamentals

## 1. What is Version Control System (VCS)?

A Version Control System (VCS) is a tool used to track changes in files and source code over time.

### Why Do We Need VCS?

Without VCS:

```text
LoanCalculator.java
LoanCalculator_final.java
LoanCalculator_final_v2.java
LoanCalculator_latest.java
```

Problems:

* No history tracking
* Difficult collaboration
* Hard to identify who changed what
* Difficult to restore older versions

With Git:

```text
Version 1
Version 2
Version 3
Version 4
```

Git tracks:

* Who made the change
* When the change was made
* What was changed
* Why it was changed

---

## 2. Types of Version Control Systems

### Local VCS

All versions are stored on the local machine.

```text
Laptop
 ├── Version 1
 ├── Version 2
 └── Version 3
```

Advantages:

* Simple
* No internet required

Disadvantages:

* No collaboration
* Data loss if machine crashes

---

### Centralized VCS (CVCS)

A central server stores all code.

```text
Developer A
      |
Developer B ----> Central Server
      |
Developer C
```

Examples:

* SVN
* CVS

Advantages:

* Easy management
* Central control

Disadvantages:

* Single point of failure
* Server crash affects everyone

---

### Distributed VCS (DVCS)

Every developer has a complete copy of the repository.

```text
Developer A Repository
Developer B Repository
Developer C Repository
          |
      Remote Repository
```

Examples:

* Git
* Mercurial

Advantages:

* Offline commits
* Faster operations
* Better backup
* No single point of failure

Git is a Distributed Version Control System (DVCS).

---

# 3. Git Architecture

Git works using four areas:

```text
Working Directory
      ↓ git add
Staging Area (Index)
      ↓ git commit
Local Repository
      ↓ git push
Remote Repository (GitHub)
```

---

## Working Directory

Where files are created or modified.

Example:

```bash
echo "Hello" > file1.txt
```

State:

```text
Working Directory
    |
    └── file1.txt
```

---

## Staging Area

Used to prepare files for the next commit.

Command:

```bash
git add file1.txt
```

Meaning:

> Include this file in the next commit.

---

## Local Repository

Stores commits locally on the developer machine.

Command:

```bash
git commit -m "Created file1"
```

Meaning:

> Save a permanent version of the project.

---

## Remote Repository

Stores code on GitHub, GitLab, Bitbucket, Azure Repos, etc.

Command:

```bash
git push origin main
```

Meaning:

> Upload local commits to the remote repository.

---

# 4. Git Workflow

```text
Create File
     ↓
Working Directory
     ↓ git add
Staging Area
     ↓ git commit
Local Repository
     ↓ git push
Remote Repository (GitHub)
```

---

## Real Example

```bash
echo "Login Module" > LoginService.java

git add LoginService.java

git commit -m "Added login feature"

git push origin main
```

---

# 5. Important Git Commands

## git init

Initializes a Git repository.

```bash
git init
```

Creates:

```text
.git/
```

The .git directory stores:

* Commit history
* Branches
* Configurations
* References

Without .git, the folder is just a normal directory.

---

## git status

Shows repository status.

```bash
git status
```

Used to check:

* Untracked files
* Staged files
* Modified files
* Current branch status

---

## git add

Moves files from Working Directory to Staging Area.

```bash
git add file1.txt
```

or

```bash
git add .
```

---

## git commit

Creates a snapshot/version of staged files.

```bash
git commit -m "Created file1.txt"
```

A commit is a saved version of the project.

---

## git push

Uploads commits to GitHub.

```bash
git push origin main
```

---

## git clone

Copies an entire remote repository to the local machine.

```bash
git clone <repository-url>
```

Copies:

* Source code
* Commit history
* Branches
* Configuration

Example:

```bash
git clone https://github.com/company/project.git
```

---

## git fetch

Checks and downloads incremental changes from the remote repository.

```bash
git fetch
```

Characteristics:

* Updates local repository information
* Does NOT update working directory
* Does NOT merge changes automatically

Use when you want to inspect changes before merging.

---

## git pull

Checks and downloads changes from the remote repository and merges them into the current branch.

```bash
git pull
```

Equivalent to:

```bash
git fetch
git merge
```

Characteristics:

* Updates local repository
* Updates working directory
* Automatically merges changes

Best practice:
Use git pull regularly to keep your local repository synchronized with the remote repository.

---

## Fork

Fork means creating a copy of one remote repository into another remote repository.

```text
Original GitHub Repository
            ↓
           Fork
            ↓
Your GitHub Repository
```

Difference:

```text
Fork  : Remote → Remote

Clone : Remote → Local
```

---

# 6. Repository Inspection Commands

## git log

Displays commit history.

```bash
git log
```

Shows:

* Commit ID
* Author
* Date
* Commit message

---

## ls

Linux command to list files and directories.

```bash
ls
```

Example:

```text
file1.txt
file2.txt
notes.txt
```

---

## git ls-files

Displays files currently tracked by Git.

```bash
git ls-files
```

Example:

Folder:

```text
file1.txt
file2.txt
notes.txt
```

Tracked:

```text
file1.txt
file2.txt
```

Output:

```bash
git ls-files
```

```text
file1.txt
file2.txt
```

---

# 7. Git Configuration

Every commit contains:

```text
Author Name
Author Email
```

Git uses configuration to identify the author.

---

## Global Configuration

Applies to all repositories on the machine.

```bash
git config --global user.name "Micah"

git config --global user.email "micah@gmail.com"
```

One-time setup.

---

## Local Configuration

Applies only to the current repository.

```bash
git config user.name "Micah"

git config user.email "micah@gmail.com"
```

Overrides global configuration for that repository.

---

# 8. Complete Flow of Execution

### Install Git

Install Git Client.

---

### Create Repository

```bash
mkdir pl-devops-1506

cd pl-devops-1506

mkdir repo1

cd repo1
```

---

### Initialize Repository

```bash
git init
```

---

### Configure Git

```bash
git config --global user.name "Micah"

git config --global user.email "micah@gmail.com"
```

---

### Create File

```bash
echo "rec1" >> file1.txt
```

---

### Check Status

```bash
git status
```

---

### Add File to Staging Area

```bash
git add file1.txt
```

---

### Commit Changes

```bash
git commit -m "Created file1.txt"
```

---

### View Commit History

```bash
git log
```

---

# Interview Questions

1. What is Git?
2. What is Version Control System (VCS)?
3. Difference between Local, Centralized and Distributed VCS?
4. What is a Git Repository?
5. What is the purpose of .git directory?
6. Explain Git Architecture.
7. Difference between Working Directory and Staging Area?
8. Difference between git add and git commit?
9. Difference between git fetch and git pull?
10. Difference between Fork and Clone?
11. Difference between Global and Local Configuration?
12. What does git ls-files do?
13. What information is displayed by git log?
14. Why is Git called a Distributed Version Control System?
