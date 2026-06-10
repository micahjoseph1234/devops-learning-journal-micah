# Day 7 Assignment - Remote Server Access Lab

## Main Objective

Establish passwordless SSH connectivity between two Linux servers and transfer files using SCP.

---

## Task 1

Launch two Ubuntu EC2 instances.

Name them:

* VM1 (Source Machine)
* VM2 (Target Machine)

Record:

* VM1 Public IP
* VM1 Private IP
* VM2 Public IP
* VM2 Private IP

---

## Task 2

Connect to both servers using SSH from your Mac.

Verify:

* whoami
* pwd
* hostname -I

---

## Task 3

On VM1:

Create Linux user:

```bash
useradd devopsadmin -s /bin/bash -m -d /home/devopsadmin
```

Switch user:

```bash
su - devopsadmin
```

Verify:

```bash
whoami
pwd
```

---

## Task 4

On VM1:

Generate SSH keys.

```bash
ssh-keygen -t ecdsa -b 521
```

Verify:

```bash
cd ~/.ssh

ls
```

Expected files:

* id_ecdsa
* id_ecdsa.pub

---

## Task 5

Display public key.

```bash
cat ~/.ssh/id_ecdsa.pub
```

Copy the complete key.

Save it temporarily.

---

## Task 6

On VM2:

Create Linux user:

```bash
useradd adminuser1 -s /bin/bash -m -d /home/adminuser1
```

Switch user:

```bash
su - adminuser1
```

Verify:

```bash
whoami
pwd
```

---

## Task 7

On VM2:

Create SSH directory.

```bash
mkdir ~/.ssh

cd ~/.ssh
```

Create file:

```bash
vi authorized_keys
```

Paste the public key copied from VM1.

Save and exit.

---

## Task 8

On VM2:

Secure SSH files.

```bash
chmod 600 ~/.ssh/*
```

Verify:

```bash
ls -l ~/.ssh
```

---

## Task 9

From VM1:

Login to VM2 using SSH.

```bash
ssh adminuser1@<VM2_PRIVATE_IP>
```

Verify:

```bash
whoami
pwd
```

---

## Task 10

Return to VM1.

Create file:

```bash
echo "Deployment Started" > sourcefile.txt
```

Verify:

```bash
cat sourcefile.txt
```

---

## Task 11

Copy file from VM1 to VM2.

```bash
scp sourcefile.txt adminuser1@<VM2_PRIVATE_IP>:/home/adminuser1
```

---

## Task 12

Login to VM2.

Verify file transfer.

```bash
ls

cat sourcefile.txt
```

---

## Task 13

Create another file on VM1.

```bash
touch app.war
```

Transfer it to VM2 using SCP.

Verify transfer.

---

## Task 14

Create directory:

```bash
mkdir deployment_files
```

Create 3 files inside it.

Transfer the complete directory to VM2 using SCP.

Verify transfer on VM2.

---

## Task 15

Delete:

* sourcefile.txt
* app.war

from VM2.

Verify deletion.

---

## Task 16

From VM1:

Logout and reconnect to VM2.

Verify that passwordless SSH still works.

```bash
ssh adminuser1@<VM2_PRIVATE_IP>
```

---

## Final Verification

Successfully completed:

* User Creation
* SSH Key Generation
* authorized_keys Configuration
* Passwordless SSH Login
* File Transfer using SCP
* Directory Transfer using SCP
* Remote Server Access
