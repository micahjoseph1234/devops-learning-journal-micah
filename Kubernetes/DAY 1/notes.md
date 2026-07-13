# Kubernetes - Day 1 Notes

# 1. What is Kubernetes?

Kubernetes (K8s) is an **open-source Container Orchestration Platform** used to deploy, manage, scale, and monitor containerized applications.

### Why Kubernetes?

Docker can create and run containers, but it cannot efficiently manage thousands of containers running across multiple servers. Kubernetes solves this problem by automating container management.

### Features

* Container Orchestration
* High Availability (HA)
* Auto Scaling
* Load Balancing
* Self-Healing
* Rolling Updates & Rollbacks
* Supports Microservice Architectures

---

# 2. Why Kubernetes is Needed

Without Kubernetes:

* Containers must be managed manually.
* Failed containers require manual intervention.
* Scaling applications is difficult.
* Managing hundreds of servers becomes complex.

With Kubernetes:

* Automatically recreates failed containers.
* Distributes traffic among healthy containers.
* Automatically scales applications based on demand.
* Schedules applications across multiple machines.

---

# 3. Microservices and Kubernetes

Modern applications are divided into multiple independent services.

Example:

* Frontend
* Authentication Service
* Product Service
* Order Service
* Payment Service
* Notification Service

Each microservice:

* Has its own Docker Image
* Runs inside one or more Pods
* Can be scaled independently

Example:

Product Service

* Product Pod 1
* Product Pod 2
* Product Pod 3

These Pods are usually distributed across multiple Worker Nodes to provide High Availability.

---

# 4. Kubernetes Cluster

A Kubernetes Cluster consists of:

* Control Plane (Master Node)
* One or more Worker Nodes

```text
              Kubernetes Cluster

        +---------------------------+
        |      Control Plane        |
        +---------------------------+
                  │
      ┌───────────┼───────────┐
      │           │           │
 Worker 1     Worker 2     Worker 3
```

### Control Plane Responsibilities

* Makes scheduling decisions
* Maintains cluster state
* Monitors worker nodes
* Manages deployments

### Worker Node Responsibilities

* Runs Pods
* Runs Containers
* Executes application workloads

---

# 5. Kubernetes Architecture Components

## API Server

* Entry point of Kubernetes.
* Receives all requests from `kubectl`.
* Validates requests.
* Communicates with all Kubernetes components.

---

## ETCD

* Distributed key-value database.
* Stores the complete cluster state.
* Known as the **Single Source of Truth**.

Stores:

* Pods
* Nodes
* Deployments
* Services
* ConfigMaps
* Secrets
* Cluster configuration

---

## Scheduler

Responsible for selecting the best Worker Node for a new Pod.

Decision factors include:

* CPU
* Memory
* Node health
* Available resources
* Scheduling constraints

---

## Controller Manager

Continuously compares:

* Desired State
* Actual State

If a Pod fails, it creates a replacement Pod to maintain the desired number of replicas.

---

## Kubelet

Runs on every Worker Node.

Responsibilities:

* Receives instructions from the API Server.
* Creates Pods.
* Monitors Pod health.
* Reports status back to the Control Plane.

---

## Kube Proxy

Responsible for Pod networking.

Functions:

* Assigns networking rules.
* Routes traffic to Pods.
* Enables communication between Pods and Services.

---

## Container Runtime (containerd)

Responsible for:

* Pulling container images.
* Creating containers.
* Starting and stopping containers.

---

# 6. Kubernetes Terminologies

## Kubernetes Cluster

Complete Kubernetes environment consisting of:

* Control Plane
* Worker Nodes

---

## Pod

The **smallest deployable and schedulable unit** in Kubernetes.

A Pod may contain:

* One Container (most common)
* Multiple tightly coupled containers (e.g., sidecar pattern)

Kubernetes schedules Pods, not individual containers.

---

## Container Image

A static, read-only blueprint of an application.

Characteristics:

* Non-executable
* Built using a Dockerfile
* Consists of multiple image layers

---

## Container

A running instance of a Container Image.

Consumes:

* CPU
* Memory
* Network

---

## Container Registry

Stores and manages container images.

Examples:

* Docker Hub
* Amazon ECR
* Azure Container Registry (ACR)
* Google Artifact Registry

---

## Container Repository

A collection of related images inside a Registry.

Example:

Registry:

Docker Hub

Repository:

```
micah/product-service
```

Tags:

* v1
* v2
* latest

---

## kubectl

Command Line Interface (CLI) used to interact with the Kubernetes API Server.

Common Commands:

```bash
kubectl get pods
kubectl get nodes
kubectl describe pod
kubectl logs
kubectl apply -f deployment.yaml
kubectl delete pod <pod-name>
```

---

## Kubelet

Node agent responsible for creating and monitoring Pods on Worker Nodes.

---

## kubeadm

Tool used to install and initialize a Kubernetes Cluster.

Common Commands:

```bash
kubeadm init
```

Initializes the Control Plane.

```bash
kubeadm join
```

Adds Worker Nodes to the cluster.

---

# 7. End-to-End Deployment Flow

```text
Developer
      │
      ▼
Spring Boot Application
      │
      ▼
Dockerfile
      │
      ▼
Docker Image
      │
      ▼
Push Image to Registry
      │
      ▼
kubectl apply deployment.yaml
      │
      ▼
API Server
      │
      ▼
ETCD (Stores Desired State)
      │
      ▼
Scheduler
      │
      ▼
Worker Node Selected
      │
      ▼
Kubelet
      │
      ▼
Container Runtime (containerd)
      │
      ▼
Pod Created
      │
      ▼
Application Running
```

---

# 8. Important Interview Questions

### Q1. Why do we need Kubernetes if Docker already exists?

Docker creates and runs containers, whereas Kubernetes manages containers across multiple machines by providing scheduling, auto-scaling, self-healing, load balancing, and high availability.

---

### Q2. Why does Kubernetes deploy Pods instead of Containers?

A Pod is the smallest deployable unit in Kubernetes. It provides a shared network namespace, shared storage (if configured), and lifecycle management for one or more tightly coupled containers.

---

### Q3. What is ETCD?

ETCD is a distributed key-value database that stores the entire state of the Kubernetes cluster. It is known as the **Single Source of Truth**.

---

### Q4. What is the difference between an Image and a Container?

| Image                  | Container             |
| ---------------------- | --------------------- |
| Static                 | Running               |
| Read-only              | Executable            |
| Blueprint              | Running instance      |
| Built using Dockerfile | Created from an Image |

---

### Q5. What is the difference between a Registry and a Repository?

| Registry                 | Repository                         |
| ------------------------ | ---------------------------------- |
| Stores many repositories | Stores versions of one application |
| Example: Docker Hub      | Example: `micah/product-service`   |

---

# 9. Quick Revision (2 Minutes)

* Kubernetes = Container Orchestration Platform.
* Cluster = Control Plane + Worker Nodes.
* Pods are the smallest deployable units.
* Kubernetes schedules Pods, not Containers.
* API Server = Entry point.
* ETCD = Cluster database (Single Source of Truth).
* Scheduler = Chooses the best Worker Node.
* Controller Manager = Maintains desired state.
* Kubelet = Node agent that creates and monitors Pods.
* Kube Proxy = Handles Pod networking.
* Container Runtime = Pulls images and runs containers.
* kubectl = CLI to interact with Kubernetes.
* kubeadm = Tool used to set up a Kubernetes cluster.
