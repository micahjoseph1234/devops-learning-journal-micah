# Kubernetes Day 1 – Interview Notes

## Topics Covered
- Managed Kubernetes (EKS, AKS, GKE)
- Self-managed Kubernetes (kubeadm)
- Kubernetes Cluster Architecture
- Master vs Worker Nodes
- Linux Preparation
- Swap
- containerd & CRI
- OverlayFS & br_netfilter
- IP Forwarding
- SystemdCgroup
- kubeadm
- kubelet
- kubectl
- kubeadm init
- admin.conf
- Flannel (CNI)
- kubeadm join

## Managed Kubernetes
### Self-managed
- You manage:
  - API Server
  - ETCD
  - Scheduler
  - Controller Manager
  - Upgrades
  - Certificates
  - Networking

### Managed
| Cloud | Kubernetes | Registry |
|---|---|---|
| AWS | EKS | ECR |
| Azure | AKS | ACR |
| GCP | GKE | GCR / Artifact Registry |

### EKS vs ECS
- EKS = Managed Kubernetes
- ECS = AWS proprietary orchestrator (not Kubernetes)

## Cluster Architecture
### Control Plane
- API Server
- ETCD
- Scheduler
- Controller Manager

### Worker Node
- kubelet
- kube-proxy
- containerd

## Linux Preparation
- Ubuntu
- Unique Hostname
- Security Groups
- Disable Swap
- containerd
- overlay
- br_netfilter
- IP Forwarding
- SystemdCgroup=true

### Why Disable Swap?
Kubernetes requires predictable memory management. Swap moves inactive memory pages to disk, making scheduling and performance less predictable.

### containerd
Responsible for:
- Pulling images
- Creating containers
- Starting/stopping containers
- Working with Kubernetes through CRI

## kubeadm
Responsible for:
- Preflight checks
- Certificates
- ETCD
- API Server
- Scheduler
- Controller Manager
- Join Token
- admin.conf

## admin.conf
Provides kubectl with:
- Cluster endpoint
- Authentication
- Certificates
- User context

## Flannel
- CNI plugin
- Enables Pod-to-Pod networking across nodes
- Uses Pod CIDR (10.244.0.0/16)

## kubeadm join
- Authenticates Worker
- Registers Node
- kubelet starts heartbeats
- Node becomes Ready
