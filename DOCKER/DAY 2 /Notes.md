# Day 3 - Docker (Image Creation & Dockerfile)

## Topics Covered

- Docker Commit
- Docker Hub
- Docker Build
- Dockerfile
- Dockerfile Instructions
- Docker Image Layers
- Docker Build Cache
- Docker Commit vs Docker Build
- Dockerfile vs Docker Compose

---

# 1. Docker Commit

## Definition

Docker Commit is used to create a **new Docker Image** from an existing Container.

It takes a snapshot of the current state of the container.

```
Container
      |
docker commit
      |
      ▼
Docker Image
```

---

## Why do we use it?

Suppose we manually installed:

- Git
- Java
- Maven

inside a running Ubuntu container.

Instead of repeating these installations again and again, we create a new reusable image.

---

## Syntax

```bash
docker commit <container_id> <dockerhub_username>/<image_name>:<tag>
```

Example

```bash
docker commit 13512cdaeac9 micahjoseph123/java-build:v1
```

---

## Verify

```bash
docker images
```

---

## Create Container from New Image

```bash
docker run -it micahjoseph123/java-build:v1 bash
```

Verify

```bash
java --version
mvn --version
git --version
```

---

## Advantages

- Easy
- Fast
- Good for testing
- Creates reusable image

---

## Disadvantages

- Manual process
- Not version controlled
- Difficult to reproduce
- Not suitable for CI/CD

---

# Docker Commit Workflow

```
Ubuntu Image

↓

Container

↓

Install Java

↓

Install Maven

↓

Install Git

↓

docker commit

↓

java-build:v1
```

---

# Interview Question

Why is Docker Commit not used in Production?

Answer:

Because it is manual, not reproducible, and the installation steps are not documented.

Companies use Dockerfile instead.

---

# 2. Docker Hub

Docker Hub is a Container Registry used to store Docker Images.

Similar to GitHub.

| GitHub | Docker Hub |
|---------|------------|
| Stores Source Code | Stores Docker Images |

---

## Login

```bash
docker login
```

---

## Push Image

```bash
docker push micahjoseph123/java-build:v1
```

---

## Pull Image

```bash
docker pull micahjoseph123/java-build:v1
```

---

## Workflow

```
Developer

↓

Docker Build / Docker Commit

↓

Docker Image

↓

Docker Hub

↓

Developer

↓

docker pull

↓

Container
```

---

# Important

docker commit

Creates Image

docker push

Uploads Image

They are different operations.

---

# 3. Docker Build

## Definition

Docker Build creates a Docker Image using a Dockerfile.

Instead of manually configuring a container, developers write instructions.

---

## Workflow

```
Dockerfile

↓

docker build

↓

Docker Image
```

---

## Syntax

```bash
docker build -t micahjoseph123/java-build:v2 .
```

---

## Meaning

docker build

Creates Image

-t

Image Tag

.

Current Directory (Docker searches for Dockerfile)

---

# Docker Commit vs Docker Build

| Docker Commit | Docker Build |
|---------------|--------------|
| Source = Container | Source = Dockerfile |
| Manual | Automated |
| Snapshot | Recipe |
| Not reproducible | Reproducible |
| Not version controlled | Version controlled |
| Used rarely | Industry Standard |

---

# Why Dockerfile?

Dockerfile stores every installation step as code.

Benefits

- Repeatable
- Automated
- Version Controlled
- Easy Maintenance
- Used in CI/CD

---

# Dockerfile

Dockerfile is a text file containing instructions to create a Docker Image.

---

# Dockerfile Instructions

---

## FROM

Purpose

Defines Base Image.

Example

```dockerfile
FROM ubuntu
```

Without FROM Docker doesn't know where to start.

---

## RUN

Purpose

Executes commands during image build.

Example

```dockerfile
RUN apt update -y

RUN apt install -y git
```

Important

RUN executes during

docker build

NOT

docker run

Each RUN creates a new Image Layer.

---

## COPY

Purpose

Copies files from Host Machine to Docker Image.

Example

```dockerfile
COPY target/banking.war /usr/local/tomcat/webapps/
```

Flow

```
Host

↓

Docker Image

↓

Container
```

Used for

- WAR
- JAR
- Config Files
- Source Code

---

## WORKDIR

Purpose

Sets default working directory.

Example

```dockerfile
WORKDIR /usr/local/tomcat/webapps
```

Benefits

- Avoid repeated cd
- Cleaner Dockerfile
- Automatically creates directory if missing

---

## ENV

Purpose

Creates Environment Variables.

Example

```dockerfile
ENV APP_ENV=QA

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

Available inside running container.

---

## ARG

Purpose

Defines Build-Time Variables.

Example

```dockerfile
ARG APP_VERSION=1.0
```

Build

```bash
docker build --build-arg APP_VERSION=2.0 .
```

ARG is NOT available inside running container.

---

## EXPOSE

Purpose

Documents application port.

Example

```dockerfile
EXPOSE 8080
```

Important

EXPOSE does NOT publish ports.

Need

```bash
docker run -p 8085:8080
```

---

## CMD

Purpose

Default startup command.

Example

```dockerfile
CMD ["bash"]
```

Can be overridden.

Example

```bash
docker run image ls
```

CMD becomes

```
ls
```

---

## ENTRYPOINT

Purpose

Defines fixed executable.

Example

```dockerfile
ENTRYPOINT ["java","-jar"]

CMD ["banking.jar"]
```

Container executes

```
java -jar banking.jar
```

Changing command

```bash
docker run image payroll.jar
```

Executes

```
java -jar payroll.jar
```

ENTRYPOINT remains.

CMD changes.

---

# CMD vs ENTRYPOINT

| CMD | ENTRYPOINT |
|------|------------|
| Default Command | Fixed Executable |
| Can be replaced | Normally remains fixed |
| Runtime default | Runtime executable |

---

# ENV vs ARG

| ENV | ARG |
|------|-----|
| Runtime Variable | Build Variable |
| Available inside Container | Available only during Build |
| Stored in Image | Not available after Build |

---

# COPY vs ADD

COPY

- Host → Image
- Preferred
- Predictable

ADD

- Host → Image
- URL Support
- Auto Extract tar files

Companies prefer COPY.

---

# Docker Image Layers

Every Dockerfile instruction creates a new layer.

```
Layer 6

CMD

↓

Layer 5

EXPOSE

↓

Layer 4

COPY

↓

Layer 3

RUN Maven

↓

Layer 2

RUN Git

↓

Layer 1

FROM Ubuntu
```

---

# Docker Build Cache

Docker caches layers.

If nothing changes

Docker reuses previous layers.

Benefits

- Faster Builds
- Less Download
- Better Performance

---

# Dockerfile vs Docker Compose

Dockerfile

Creates Docker Image.

```
Dockerfile

↓

docker build

↓

Image
```

Docker Compose

Runs Multiple Containers.

```
compose.yaml

↓

docker compose up

↓

Containers
```

---

# Real Production Workflow

```
Developer

↓

Source Code

↓

Maven Build

↓

banking.war

↓

Dockerfile

↓

docker build

↓

Docker Image

↓

Docker Hub

↓

docker pull

↓

docker run

↓

QA

↓

Production
```

---

# Commands Practiced

```bash
docker commit

docker images

docker run

docker login

docker push

docker pull

docker build

docker build -t

docker run -it

docker run -p

docker run image ls
```

---

# Interview Questions

1. Docker Commit vs Docker Build

2. Dockerfile vs Docker Compose

3. CMD vs ENTRYPOINT

4. ENV vs ARG

5. COPY vs ADD

6. EXPOSE vs -p

7. Why is Dockerfile preferred over Docker Commit?

8. What is Docker Build Cache?

9. Why does every Dockerfile start with FROM?

10. Why does every RUN create a new Image Layer?

11. Why is WORKDIR better than repeatedly using cd?

12. Why is COPY preferred over ADD?

13. What is the purpose of Docker Hub?

14. Why is ARG not available inside a running container?

15. What is the difference between Image and Container?

---

# Key Takeaways

- Docker Commit = Snapshot of Container
- Docker Build = Image from Dockerfile
- Dockerfile = Infrastructure as Code
- Docker Hub = Image Registry
- RUN executes during Build
- CMD executes during Container Start
- ENTRYPOINT defines fixed executable
- EXPOSE documents Container Port
- -p publishes Container Port
- WORKDIR changes working directory
- ENV is Runtime Variable
- ARG is Build-Time Variable
- Docker Build is the Industry Standard
