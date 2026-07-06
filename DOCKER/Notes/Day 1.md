# Day 1 - Docker Fundamentals & Containerization
**Date:** 6th July 2026

---

# Table of Contents

1. What is Containerization?
2. Virtual Machines vs Containers
3. Namespaces and cgroups
4. Docker Terminologies
5. Docker Architecture
6. Installing Docker
7. Docker CLI Commands
8. Docker Images and Containers
9. Docker Execution Modes
10. Docker Container Lifecycle
11. Docker `exec` vs `attach`
12. Understanding PID 1
13. Important Interview Questions
14. Hands-on Lab

---

# 1. What is Containerization?

Containerization is the process of packaging an application along with all its dependencies into a single unit called a **Container Image**.

## Example

```text
web_app.war
JDK 17
Tomcat 8.5
Libraries
Configurations
     ↓
Docker Image
     ↓
Docker Container
```

## Benefits

- Eliminates "Works on My Machine" issues.
- Environment consistency.
- Faster deployments.
- Lightweight compared to Virtual Machines.
- Portable across environments.

---

# 2. Virtual Machines vs Containers

| Virtual Machine | Container |
|-----------------|------------|
| Hardware-level virtualization | OS-level virtualization |
| Uses Hypervisor | Uses Container Engine |
| Runs full OS | Runs only application |
| Heavyweight | Lightweight |
| Slow startup | Fast startup |
| Consumes more resources | Consumes fewer resources |
| Requires Guest OS | Shares Host OS Kernel |

---

## Architecture

### Virtual Machine

```text
Application
Guest OS
Hypervisor
Host OS
Hardware
```

### Container

```text
Application
Libraries
Docker Engine
Host OS
Hardware
```

---

# 3. Namespaces and cgroups

Containers are built using two Linux Kernel features.

---

## Namespaces

Provide **Isolation**.

Each container gets its own:

- Processes
- Network
- Filesystem
- Hostname
- Users

### Types of Namespaces

- PID Namespace
- Network Namespace
- Mount Namespace
- IPC Namespace
- UTS Namespace
- User Namespace

### Interview Definition

> Namespaces provide isolation between containers.

---

## cgroups (Control Groups)

Provide **Resource Management**.

Controls:

- CPU
- Memory
- Disk I/O
- Network bandwidth

### Interview Definition

> cgroups control and limit the resources used by containers.

---

## One-liner

```text
Namespaces = Isolation
cgroups = Resource Control
```

---

# 4. Docker Terminologies

---

## Containerization

Packaging applications along with dependencies.

---

## Container Engine

Software used to create and manage containers.

Examples:

- Docker Engine
- containerd
- CRI-O

---

## Container Image

- Static
- Read-only
- Non-executable
- Blueprint of a container

Example:

```text
web_app_image:v1.0
```

---

## Container

A running instance of an image.

---

## Container Registry

Stores container images.

Example:

- Docker Hub

https://hub.docker.com/

---

## Repository

A subset inside a registry.

Example:

```text
micah/webapp
micah/python-app
```

---

# 5. Docker Architecture

```text
Docker CLI
      ↓
Docker Daemon (dockerd)
      ↓
Images
Containers
Networks
Volumes
```

---

# 6. Installing Docker

```bash
sudo -i
apt update
apt install docker.io -y
```

Verify:

```bash
docker --version
docker info
```

---

# 7. Docker CLI Commands

---

## Docker Version

```bash
docker --version
```

---

## Docker Information

```bash
docker info
```

---

## List Images

```bash
docker images
```

---

## Running Containers

```bash
docker ps
```

---

## All Containers

```bash
docker ps -a
```

---

# 8. Docker Images and Containers

---

## Pull an Image

```bash
docker pull ubuntu
```

### What happens?

```text
Docker Hub
      ↓
Downloads Image
      ↓
Stores Locally
```

---

## Run a Container

```bash
docker run ubuntu
```

### Internally

```text
docker run
=
docker pull (if image not present)
+
docker create
+
docker start
```

---

## Image vs Container

| Image | Container |
|--------|------------|
| Blueprint | Running Instance |
| Static | Dynamic |
| Read-only | Read/Write |
| Non-executable | Executable |

---

## Java Analogy

```text
Class      = Image
Object     = Container
```

---

# 9. Docker Execution Modes

---

# Foreground Mode

```bash
docker run ubuntu
docker run ubuntu sleep 20
```

### Characteristics

- Default mode
- Occupies terminal
- Shows output directly

---

# Detached Mode

```bash
docker run -d ubuntu sleep 300
```

### Characteristics

- Runs in background
- Terminal is free
- Used in production

---

# Interactive Mode

```bash
docker run -it ubuntu bash
```

### Characteristics

- Opens shell automatically
- Used for debugging and learning

---

## Meaning of -it

```text
-i = Interactive
-t = Allocate Terminal (TTY)
```

---

# Difference

| Mode | Terminal Attached | Background |
|------|------------------|------------|
| Foreground | Yes | No |
| Detached | No | Yes |
| Interactive | Yes | No |

---

# 10. Docker Container Lifecycle

```text
Image
   ↓
Create Container
   ↓
Start Container
   ↓
Running
   ↓
Stopped
   ↓
Removed
```

---

## Start Existing Container

```bash
docker start container_id
```

---

## Stop Container

```bash
docker stop container_id
```

---

## Remove Container

```bash
docker rm container_id
```

---

## Remove Image

```bash
docker rmi image_id
```

---

# Important Rule

An image cannot be removed if any container is using it.

```text
Stop Container
     ↓
Remove Container
     ↓
Remove Image
```

---

# 11. Docker exec vs Docker attach

---

# docker exec

```bash
docker exec -it container_id bash
```

Creates a **new process** inside a running container.

Example:

```text
PID 1  sleep 300
PID 7  bash
PID 8  ps
```

Exiting bash:

```text
bash exits
sleep still running
container continues running
```

---

# docker attach

```bash
docker attach container_id
```

Attaches to the existing main process (PID 1).

Exiting the main process:

```text
PID 1 exits
Container stops
```

---

## Difference

| docker exec | docker attach |
|-------------|----------------|
| Creates new process | Connects to existing process |
| Safer | Can stop container |
| Used frequently | Rarely used |

---

# 12. Understanding PID 1

Containers exist because of their main process.

---

## Example

```bash
docker run -d ubuntu sleep 300
```

Inside container:

```text
PID 1 sleep 300
```

Now:

```bash
docker exec -it container_id bash
```

Processes:

```text
PID 1 sleep 300
PID 7 bash
PID 8 ps
```

---

## Meaning

### PID 1

Main container process.

### PID 7

New shell created by docker exec.

### PID 8

Temporary process created when executing `ps`.

---

## Most Important Concept

```text
Container lives as long as PID 1 lives.
```

If PID 1 exits:

```text
Container stops.
```

---

# Why does `docker run ubuntu` exit immediately?

Because:

```text
PID 1 = /bin/bash
```

When bash exits:

```text
Container exits.
```

---

# 13. Important Interview Questions

---

## What is Containerization?

Packaging application and dependencies together.

---

## Difference between VM and Container?

VM virtualizes hardware.

Container virtualizes operating system.

---

## What are Namespaces?

Provide isolation.

---

## What are cgroups?

Provide resource limits.

---

## Difference between Image and Container?

Image is a blueprint.

Container is a running instance.

---

## Difference between docker pull and docker run?

```text
docker pull
=
Download image only.

docker run
=
Pull (if needed)
+
Create container
+
Start container.
```

---

## Difference between docker run and docker start?

```text
docker run
=
Create + Start

docker start
=
Start existing container
```

---

## Difference between docker exec and docker attach?

```text
exec
=
New process inside container

attach
=
Connect to existing process
```

---

## Why do containers stop?

Because their PID 1 process exits.

---

## Why can't an image be deleted?

Because one or more containers are referencing it.

---

# 14. Hands-on Lab

```bash
docker --version
docker info

docker images
docker ps
docker ps -a

docker pull ubuntu
docker images

docker run ubuntu
docker ps -a

docker run ubuntu sleep 20
docker run -d ubuntu sleep 300
docker ps

docker run -it ubuntu bash
exit

docker start <container-id>

docker exec -it <container-id> bash
ps -ef
exit

docker stop <container-id>
docker rm <container-id>
docker rmi ubuntu
```

---

# Final Revision

```text
Image = Blueprint
Container = Running Instance
Container = Isolated Process
Namespaces = Isolation
cgroups = Resource Limits
docker run = pull + create + start
docker exec = new process
docker attach = connect to PID 1
Container lives as long as PID 1 lives
```
