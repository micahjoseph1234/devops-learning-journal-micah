# Linux Fundamentals - Day 1

## SSH into EC2

Connect to an EC2 instance:

```bash
ssh -i MICAH.pem ubuntu@Public-IP
```

---

## File Permissions

Secure PEM file:

```bash
chmod 400 MICAH.pem
```

Verify permissions:

```bash
ls -l MICAH.pem
```

---

## User Commands

Current logged-in user:

```bash
whoami
```

Become root user:

```bash
sudo -i
```

---

## Package Management (Ubuntu)

Refresh package catalog:

```bash
apt update
```

Install Git:

```bash
apt install git -y
```

Install Nginx:

```bash
apt install nginx -y
```

Install Java 17 Runtime:

```bash
apt install openjdk-17-jre -y
```

Upgrade installed packages:

```bash
apt upgrade
```

---

## Verify Installed Software

Git version:

```bash
git --version
```

Java version:

```bash
java -version
```

Nginx version:

```bash
nginx -v
```

Find executable location:

```bash
which git
which nginx
```

---

## Nginx Service Management

Check status:

```bash
systemctl status nginx
```

Start service:

```bash
systemctl start nginx
```

Stop service:

```bash
systemctl stop nginx
```

Restart service:

```bash
systemctl restart nginx
```

Enable at boot:

```bash
systemctl enable nginx
```

Disable at boot:

```bash
systemctl disable nginx
```

---

# Concepts Learned

## Linux

* Linux = Server Operating System
* Kernel = Brain of Linux

## Ubuntu

* Package manager = apt

## SSH

* Uses Port 22

## File Permissions

```bash
chmod 400 file.pem
```

Meaning:

* Owner = Read
* Group = No Access
* Others = No Access

---

# Package Management

## apt update

Refresh package catalog.

Think:

"Show me what software versions are available."

## apt install

Install new software.

Examples:

```bash
apt install git -y
apt install nginx -y
```

## apt upgrade

Upgrade existing installed packages.

---

# Services

## Standalone Packages

Examples:

* Git
* Java

Run only when invoked.

## Service Packages

Examples:

* Nginx
* Apache
* MySQL

Run continuously in the background.

Managed using:

```bash
systemctl
```

---

# Troubleshooting Rules

## SSH Error

Permission denied (publickey)

Meaning:

Authentication issue.

Check:

1. Correct PEM file
2. Correct username
3. Correct permissions

---

## SSH Error

Connection timed out

Meaning:

Network issue.

Check:

1. Security Group Port 22
2. Public IP
3. Instance State
4. Network ACL

---

## Website Not Opening

Check in order:

1. Is Nginx installed?
2. Is Nginx running?
3. Is Port 80 open?
4. Is the Public IP correct?

---

# Golden Rule

Installed?
↓
Running?
↓
Port Open?
↓
Reachable?
