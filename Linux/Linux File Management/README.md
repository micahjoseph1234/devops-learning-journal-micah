# Linux File Management

## Topics Covered

### Directory Navigation

* pwd - Present Working Directory
* cd - Change Directory
* cd / - Navigate to System Root Directory
* cd ~ - Navigate to User Home Directory
* cd .. - Move to Parent Directory
* ls - List Files and Directories
* ll - Long Listing Format

---

## Root Directory vs Home Directory

### System Root Directory

```text
/
```

Top-most directory in Linux.

All files and directories exist under the root directory.

### User Home Directory

Examples:

```text
/home/ubuntu
/root
```

Default working location for a specific user.

---

## File Operations

### Create Files

```bash
touch file1.txt
```

### Write Content

```bash
echo "Record1" > file1.txt
```

### Append Content

```bash
echo "Record2" >> file1.txt
```

### Read File

```bash
cat file1.txt
```

---

## File Editor

### VI Editor

Open/Create File:

```bash
vi sample.txt
```

Common Operations:

* i → Insert Mode
* Esc :wq → Save and Exit
* Esc :q! → Exit Without Saving

---

## Rename Files and Directories

```bash
mv oldname.txt newname.txt
```

Directory Rename:

```bash
mv olddir newdir
```

---

## Delete Files

Delete File:

```bash
rm file1.txt
```

Delete Multiple Files:

```bash
rm file1.txt file2.txt
```

Force Delete:

```bash
rm -f file1.txt
```

Delete Directory:

```bash
rm -rf directoryname
```

---

## Create Directories

```bash
mkdir demodir1
```

---

## File Permissions

Example:

```text
-rw-rw-r--
```

Permission Structure:

```text
FileType Owner Group Others
```

Permission Types:

* r → Read
* w → Write
* x → Execute

Access Levels:

* Owner
* Group
* Public (Others)

---

## Change Permissions

```bash
chmod <permission> <file>
```

Example:

```bash
chmod 400 key.pem
```

---

## User Management

Create User:

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

List Users:

```bash
cat /etc/passwd
```

List Groups:

```bash
cat /etc/group
```

---

## Commands Practiced

```bash
pwd
cd
cd /
cd ~
cd ..
ls
ll
touch
echo
cat
vi
mv
rm
mkdir
chmod
useradd
su
passwd
```

## Key Learning

* Linux file system starts from `/`
* Every user has a home directory
* Files and directories can be managed using Linux commands
* Permissions are controlled through Owner, Group and Others
* Linux users can be created and managed through command line
* SSH authentication relies on users and permissions

```
```
