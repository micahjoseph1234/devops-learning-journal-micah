# Complete Hands-on Lab Notes

**Topics Covered**
- Docker Images & Containers
- Execution Modes
- PID 1
- docker exec vs attach
- Port Mapping
- Docker Stats
- Docker Volumes
- Persistent Storage
- Real-world Deployment Scenario

---

# Lab 1 - Verify Docker Installation

## Objective

Verify Docker Engine is installed correctly.

## Commands

```bash
docker --version
docker info
```

## Why?

- docker --version → Verifies Docker CLI is installed.
- docker info → Verifies Docker Engine (daemon) is running.

---

# Lab 2 - Download an Image

## Objective

Download Ubuntu image from Docker Hub.

```bash
docker pull ubuntu
```

## Verify

```bash
docker images
```

## What happens internally?

```
Docker Hub

↓

Downloads Image Layers

↓

Stores Image Locally
```

---

# Lab 3 - Create First Container

```bash
docker run ubuntu
```

## What happened?

Ubuntu image's default command is

```
/bin/bash
```

Since no terminal was attached,

```
bash exited

↓

PID 1 exited

↓

Container stopped.
```

This is why

```
docker ps -a
```

showed

```
Exited
```

---

# Lab 4 - Interactive Mode

```bash
docker run -it ubuntu bash
```

Now Docker provides

- Keyboard
- Terminal

to Bash.

Bash waits for user input.

Container remains alive until

```
exit
```

---

# Lab 5 - Start Existing Container

```bash
docker start container_id
```

Starts an existing stopped container.

It DOES NOT create a new container.

---

# Lab 6 - Login into Running Container

```bash
docker exec -it container_id bash
```

## Internally

```
Container

PID 1
bash

↓

docker exec

↓

Creates another bash

PID 27
```

Now

```
PID 1
bash

PID 27
bash
```

Exit only kills PID 27.

Container continues running.

---

# Lab 7 - Process Verification

Inside container

```bash
ps -ef
```

Example

```
PID 1
/bin/bash

PID 27
bash

PID 35
ps
```

Observation

Container depends ONLY on PID 1.

---

# Lab 8 - Deploy Tomcat

```bash
docker run -it -p 8085:8080 tomcat:8.0
```

## Observe

Tomcat startup logs.

Container remains running because

PID 1 = catalina.sh run

---

# Lab 9 - Verify Container

```bash
docker ps
```

Observe

```
STATUS

Up
```

Meaning

Container is running.

---

# Lab 10 - Understand Port Mapping

Observe

```
0.0.0.0:8085->8080/tcp
```

Meaning

```
Host

8085

↓

Docker

↓

Container

8080
```

Browser connects to

```
http://VM-IP:8085
```

Docker forwards traffic to

```
Container:8080
```

---

# Lab 11 - Multiple Tomcat Containers

Container 1

```bash
docker run -d -p 8085:8080 tomcat
```

Container 2

```bash
docker run -d -p 8086:8080 tomcat
```

Observation

```
8085 → Container1 :8080

8086 → Container2 :8080
```

Container ports can be same.

Host ports must be unique.

---

# Lab 12 - Monitor Containers

```bash
docker stats
```

Observe

- CPU %
- Memory
- Network IO
- Block IO
- PIDS

---

# Lab 13 - Create Volume

```bash
docker volume create pl-vol1
```

Verify

```bash
docker volume ls
```

Inspect

```bash
docker volume inspect pl-vol1
```

Observe

```
Mountpoint

/var/lib/docker/volumes/pl-vol1/_data
```

---

# Lab 14 - Mount Volume

```bash
docker run -it \
--mount source=pl-vol1,destination=/pl-vol1 \
ubuntu bash
```

Meaning

```
Docker Volume

↓

Mounted to

↓

/pl-vol1
```

---

# Lab 15 - Common Mistake

Wrong

```bash
mkdir folder
```

Creates

```
/folder
```

inside container.

Deleting container deletes folder.

Correct

```bash
cd /pl-vol1

mkdir folder
```

Now folder exists inside Docker Volume.

Deleting container does NOT delete data.

---

# Lab 16 - Verify Persistence

Container 1

```
Create files inside

/pl-vol1
```

Delete Container

↓

Create Container 2

↓

Mount same volume

↓

Files still exist.

Reason

Files are stored inside Docker Volume, not container filesystem.

---

# Important Commands

```bash
docker --version

docker info

docker images

docker ps

docker ps -a

docker pull ubuntu

docker run ubuntu

docker run -it ubuntu bash

docker run -d ubuntu sleep 300

docker start container_id

docker exec -it container_id bash

docker stop container_id

docker rm container_id

docker rmi image

docker run -d -p 8085:8080 tomcat

docker stats

docker volume create pl-vol1

docker volume ls

docker volume inspect pl-vol1

docker run -it \
--mount source=pl-vol1,destination=/pl-vol1 \
ubuntu bash
```

---

# Key Learnings

Image = Blueprint

Container = Running Instance

Container = Isolated Process

Namespaces = Isolation

cgroups = Resource Control

docker run = Pull + Create + Start

docker start = Start Existing Container

docker exec = Start New Process

Container lives as long as PID 1 lives.

Volumes provide Persistent Storage.

Port Mapping exposes containers to external users.
