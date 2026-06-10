# Day 7 - Linux Remote Server Access (DevOps Perspective)

## Overview

This session focused on understanding how DevOps tools communicate with remote Linux servers using SSH and SCP. The concepts learned are heavily used in Jenkins, Ansible, Terraform, Docker, and Kubernetes environments.

---

# Why Remote Server Access?

In real-world DevOps environments, applications are built on one server and deployed to another server.

Example:

```text
Developer
    ↓
GitHub
    ↓
Build Server (Jenkins)
    ↓
Target Server (Tomcat / Nginx / Docker)
```

The Build Server creates the application artifact and sends it to the Target Server for deployment.

---

# Build Server

Purpose:

* Pull Source Code
* Build Application
* Run Tests
* Create Artifacts

Examples:

* Jenkins
* GitHub Actions
* Azure DevOps

Common Artifacts:

```text
app.war
app.jar
.exe
```

---

# Target Server

Purpose:

* Run Applications
* Host Services
* Serve End Users

Examples:

* Tomcat Server
* Nginx Server
* Docker Server
* Kubernetes Worker Node

---

# Remote Server Access Use Cases

1. Connect to another Linux Server
2. Login to another Linux Server
3. Copy files between servers
4. Install, Upgrade, or Remove packages remotely

---

# Authentication vs Authorization

## Authentication

Authentication answers:

```text
Who are you?
```

Examples:

* Password
* SSH Key
* Token

Authentication determines whether a user can log in.

---

## Authorization

Authorization answers:

```text
What can you do?
```

Examples:

* Can run Docker?
* Can install packages?
* Can access /opt?

Authorization determines what actions a user can perform after login.

---

# SSH (Secure Shell)

Purpose:

```text
Secure Remote Login
```

Default Port:

```text
22
```

Example:

```bash
ssh user@server-ip
```

SSH allows secure communication between Linux machines.

---

# SSH Key-Based Authentication

Instead of using passwords, Linux servers commonly use SSH Keys for secure and automated access.

---

## Private Key

File:

```text
id_ecdsa
```

Stored On:

```text
Source Machine
```

Purpose:

* Used during authentication
* Must never be shared

Think of it as:

```text
House Key
```

---

## Public Key

File:

```text
id_ecdsa.pub
```

Stored On:

```text
Target Machine
```

Purpose:

* Safe to share
* Used to verify the private key

Think of it as:

```text
Lock Information
```

---

## authorized_keys

Location:

```text
~/.ssh/authorized_keys
```

Purpose:

Stores trusted public keys.

Example:

```text
authorized_keys
        ↑
Contains
        ↑
id_ecdsa.pub
```

During login:

```text
Private Key
      ↓
Compared With
      ↓
authorized_keys
```

If matched:

```text
Access Granted
```

Otherwise:

```text
Access Denied
```

---

# SSH Key Authentication Flow

## Source Machine (VM1)

Contains:

```text
id_ecdsa
id_ecdsa.pub
```

---

## Target Machine (VM2)

Contains:

```text
authorized_keys
```

which stores:

```text
id_ecdsa.pub
```

---

# SCP (Secure Copy)

Purpose:

```text
Copy Files Between Linux Servers
```

---

## Local Copy

```bash
cp source.txt destination/
```

Copies files within the same machine.

---

## Remote Copy

```bash
scp source.txt user@server:/path
```

Copies files between different machines.

---

## Example

```bash
scp sourcefile.txt adminuser1@172.31.8.222:/home/adminuser1
```

Meaning:

* Copy sourcefile.txt
* Connect to remote server
* Login as adminuser1
* Store file in /home/adminuser1

---

# Remote Server Access Prerequisites

## Source Machine (VM1)

Create User:

```bash
useradd devopsadmin -s /bin/bash -m -d /home/devopsadmin
```

Switch User:

```bash
su - devopsadmin
```

Generate SSH Keys:

```bash
ssh-keygen -t ecdsa -b 521
```

Files Generated:

```text
id_ecdsa
id_ecdsa.pub
```

---

## Target Machine (VM2)

Create User:

```bash
useradd adminuser1 -s /bin/bash -m -d /home/adminuser1
```

Switch User:

```bash
su - adminuser1
```

Create SSH Directory:

```bash
mkdir ~/.ssh
cd ~/.ssh
```

Create authorized_keys:

```bash
vi authorized_keys
```

Paste contents of:

```text
id_ecdsa.pub
```

from Source Machine.

Secure Files:

```bash
chmod 600 ~/.ssh/*
```

---

# Establish SSH Connection

```bash
ssh adminuser1@172.31.8.222
```

Uses:

* Private Key from Source Machine
* Public Key stored in authorized_keys on Target Machine

---

# Transfer Files Using SCP

```bash
scp sourcefile.txt adminuser1@172.31.8.222:/home/adminuser1
```

Copies file securely from VM1 to VM2.

---

# DevOps Tool Mapping

| Tool       | Purpose             |
| ---------- | ------------------- |
| SSH        | Remote Login        |
| SCP        | File Transfer       |
| Jenkins    | Uses Private Key    |
| Ansible    | Shares Public Key   |
| Docker     | Remote Management   |
| Terraform  | Server Provisioning |
| Kubernetes | Node Communication  |

---

# Architecture Diagram

```text
VM1 (Build Server)
--------------------------------
id_ecdsa        (Private Key)
id_ecdsa.pub    (Public Key)
--------------------------------
           |
           | Copy Public Key
           V
VM2 (Target Server)
--------------------------------
authorized_keys
--------------------------------
           ^
           |
SSH Login
           |
Private Key Authentication
```

---

# Key Takeaways

* SSH is used for secure remote login.
* SCP is used for secure file transfer.
* SSH runs on Port 22.
* Private Key remains on the Source Machine.
* Public Key is copied to the Target Machine.
* authorized_keys stores trusted public keys.
* Authentication verifies identity.
* Authorization determines permissions.
* Build Servers create artifacts.
* Target Servers run applications.
* Jenkins, Ansible, Terraform, Docker, and Kubernetes rely heavily on SSH-based communication.
