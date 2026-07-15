# Kubernetes Architecture Diagrams

## Overall Flow
```text
Developer
    │
kubectl
    │
API Server
    │
+-----------------------------------------+
| ETCD | Scheduler | Controller Manager |
+-----------------------------------------+
    │
Worker Node
    │
kubelet
    │
containerd
    │
Container
    │
Pod
```

## Installation Flow
```text
Ubuntu
   │
Linux Configuration
   │
Disable Swap
   │
Install containerd
   │
Install kubeadm kubelet kubectl
   │
kubeadm init
   │
API Server
ETCD
Scheduler
Controller Manager
   │
admin.conf
   │
Install Flannel
   │
kubeadm join
   │
Ready Cluster
```

## kubectl apply Flow
```text
kubectl apply
      │
API Server
      │
ETCD (Desired State)
      │
Scheduler
      │
Worker Node
      │
kubelet
      │
containerd
      │
Container
      │
Pod Running
```
