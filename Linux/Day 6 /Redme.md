# Day 6 - Linux User Management, SSH Keys and Remote Server Access

## Topics Covered

### User Management

Create Linux User:

```bash
useradd devopsadmin -s /bin/bash -m -d /home/devopsadmin
```

Switch User:

```bash
su - devopsadmin
```

Set Password:

```bash
passwd devopsadmin
```

---

## Linux User Components

A Linux user consists of:

* Username
* Bash Shell Access
* Home Directory
* Password
* SSH Keys

Example:

```text
Username      : devopsadmin
Shell         : /bin/bash
Home Directory: /home/devopsadmin
```

---

## SSH Key Authentication

Generate SSH Key Pair:

```bash
ssh-keygen -t ecdsa -b 521
```

Generated Files:

```text
id_ecdsa       -> Private Key
id_ecdsa.pub   -> Public Key
```

View SSH Directory:

```bash
cd ~/.ssh

ls ~/.ssh
```

---

## authorized_keys

Create authorized_keys:

```bash
cat id_ecdsa.pub > authorized_keys
```

Purpose:

```text
authorized_keys contains the public key.

During SSH login:

Private Key
     ↓
Compared Against
     ↓
authorized_keys
```

---

## Secure SSH Key Permissions

```bash
chmod 600 /home/devopsadmin/.ssh/*
```

Meaning:

```text
Owner  -> Read + Write
Group  -> No Access
Others -> No Access
```

---

## Linux User Information

List Linux Users:

```bash
cat /etc/passwd
```

Purpose:

```text
Displays all Linux users
```

---

List Linux Groups:

```bash
cat /etc/group
```

Purpose:

```text
Displays all Linux groups
```

---

## User Group Management

Add Existing User To Existing Group:

```bash
usermod -aG docker devopsadmin
```

Meaning:

```text
Add user 'devopsadmin'
to group 'docker'
```

---

## Ownership Management

Change Ownership:

```bash
chown -R devopsadmin /opt/tomcat
```

Change User and Group Ownership:

```bash
chown -R devopsadmin:devopsadmin /opt/tomcat
```

Purpose:

```text
Assign ownership of files/directories
to a specific user and group.
```

---

## Authentication vs Authorization

### Authentication

```text
Who can access the server?
```

Examples:

* Password
* SSH Keys

---

### Authorization

```text
What can the user do after login?
```

Examples:

* Read files
* Modify files
* Start services
* Install software

---

## Remote Server Access

Common DevOps Tools:

* Jenkins
* Ansible
* Terraform
* Docker
* Kubernetes
* Prometheus

These tools often connect to remote Linux servers using SSH.

---

## Source Server and Target Server

### Source Server (VM1)

Create User:

```bash
useradd devopsadmin -s /bin/bash -m -d /home/devopsadmin

su - devopsadmin
```

Generate SSH Keys:

```bash
ssh-keygen -t ecdsa -b 521
```

---

### Target Server (VM2)

Create User:

```bash
useradd adminuser1 -s /bin/bash -m -d /home/adminuser1

su - adminuser1
```

Create SSH Directory:

```bash
mkdir .ssh

cd .ssh
```

Create authorized_keys:

```bash
vi authorized_keys
```

Paste:

```text
Contents of id_ecdsa.pub
from Source Server
```

Secure Permissions:

```bash
chmod 600 /home/adminuser1/.ssh/*
```

---

## Establish SSH Connection

From Source VM:

```bash
ssh adminuser1@172.31.8.222
```

Purpose:

```text
Login from VM1 to VM2
using SSH key authentication
```

---

## File Transfer Using SCP

Copy File To Remote Server:

```bash
scp /home/devopsadmin/sourcefile.txt adminuser1@172.31.8.222:/home/adminuser1
```

Purpose:

```text
Securely copy files
between Linux servers
```

---

## Shell Scripting Fundamentals

Purpose:

```text
Process Automation
```

Benefits:

* Server Administration
* User Management
* File Management
* Security Updates
* Process Management
* Scheduled Tasks

---

## Real World Use Cases

Examples:

```text
Create 50 Linux Users

Patch 5000 Servers

Start Servers at 8 AM

Stop Servers at 10 PM

Deploy Applications Automatically
```

---

## Commands Practiced

```bash
sudo -i

useradd

su -

passwd

ssh-keygen -t ecdsa -b 521

cat /etc/passwd

cat /etc/group

usermod -aG

chown -R

chmod 600

ssh

scp
```

## Key Learnings

* Linux users require username, shell and home directory.
* SSH uses public and private key authentication.
* authorized_keys stores trusted public keys.
* User permissions can be managed using groups.
* Ownership can be changed using chown.
* Remote Linux servers can be accessed using SSH.
* Files can be transferred securely using SCP.
* Shell scripting is used for automation in DevOps environments.
* Authentication determines who can log in.
* Authorization determines what actions a user can perform.

```
```
