# Day 1 Lab Assignment - Git Fundamentals

## Scenario

You have joined UBS as a DevOps Engineer.

The development team has asked you to create and manage a new repository called **banking-app**.

Your task is to initialize the repository, configure Git, create project files, maintain version history, publish the repository to GitHub, and synchronize changes made by another developer.

---

## Objective

Complete all tasks using Git CLI commands only.

---

## Task 1 - Workspace Setup

Create the following structure:

```text
git-labs/
└── banking-app/
```

Requirements:

* Create the directories
* Navigate to the banking-app directory
* Initialize Git
* Verify that the repository has been initialized correctly

---

## Task 2 - Git Configuration

Configure Git for your machine.

Requirements:

* Configure username globally
* Configure email globally
* Verify the configuration

---

## Task 3 - Create Initial Project Files

Create the following files:

```text
README.md
LoginService.java
application.properties
```

Add suitable sample content to each file.

Requirements:

* Verify the files exist
* Check repository status

---

## Task 4 - Selective Staging

The development lead wants only the following files included in the first release:

```text
README.md
LoginService.java
```

Requirements:

* Stage only the required files
* Do not stage application.properties
* Verify the staging area

---

## Task 5 - First Release Commit

Create the first commit.

Requirements:

* Use an appropriate commit message
* Verify commit history
* Verify which files are currently tracked by Git

---

## Task 6 - Configuration Update

The team now wants application.properties included.

Requirements:

* Stage the file
* Commit the change
* Verify commit history again

---

## Task 7 - Publish Repository

Create a GitHub repository named:

```text
banking-app
```

Requirements:

* Connect local repository to GitHub
* Push all commits
* Verify code is visible in GitHub

---

## Task 8 - Clone Validation

Create a second copy of the repository on your machine.

Requirements:

* Clone the repository into a separate directory
* Verify commit history
* Verify tracked files

---

## Task 9 - Simulate Another Developer

Inside the cloned repository:

Create:

```text
PaymentService.java
```

Add sample content.

Requirements:

* Stage the file
* Commit the file
* Push changes to GitHub

Assume this change was made by another developer.

---

## Task 10 - Synchronization Exercise

Return to the original repository.

Requirements:

* Check whether remote changes exist without updating local files
* Verify the latest commit information
* Confirm whether PaymentService.java exists locally

Document your observations.

---

## Task 11 - Repository Update

Synchronize the original repository with GitHub.

Requirements:

* Update local repository
* Verify PaymentService.java is available locally
* Verify commit history

---

## Task 12 - Investigation Commands

Execute commands that answer the following questions:

1. What files exist in the working directory?
2. What files are currently tracked by Git?
3. What commits exist in the repository?
4. What is the current repository status?

Record the commands used.

---

## Concept Questions

Answer in your own words:

1. What is a Distributed Version Control System?
2. What does git init do?
3. What is the purpose of the .git directory?
4. Explain the difference between Working Directory and Staging Area.
5. Explain the difference between git add and git commit.
6. Explain the difference between git commit and git push.
7. Explain the difference between git clone and git pull.
8. Explain the difference between git fetch and git pull.
9. Explain the difference between ls and git ls-files.
10. Explain the difference between Global Configuration and Local Configuration.
11. Explain the difference between Fork and Clone.

---

## Deliverables

Submit:

* All commands executed
* Screenshots of:

  * git status
  * git log
  * GitHub repository
* Answers to Concept Questions
* Repository URL
