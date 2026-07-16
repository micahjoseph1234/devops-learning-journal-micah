# Kubernetes Installation (kubeadm) - Day 1

## Goal

Set up a Kubernetes cluster using kubeadm.

---

# Overall Flow

```text
Linux Preparation
        ↓
Container Runtime (containerd)
        ↓
Kubernetes Components
(kubeadm, kubelet, kubectl)
        ↓
Initialize Cluster
(kubeadm init)
        ↓
Configure kubectl
(admin.conf)
        ↓
Install Flannel (CNI)
        ↓
Cluster Ready
        ↓
Join Worker Nodes
```

---

# Phase 1 - Linux Preparation

## Become Root

```bash
sudo -i
```

## Update Packages

```bash
apt update -y
```

## Set Hostname

### Master

```bash
hostnamectl set-hostname kmaster-node
exec bash
```

### Worker

```bash
hostnamectl set-hostname worker-node1
exec bash
```

---

## Disable Swap

### Temporary

```bash
swapoff -a
```

### Permanent

```bash
sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

---

# Phase 2 - Install containerd

## Load Kernel Modules

```bash
modprobe overlay
modprobe br_netfilter
```

---

## Persist Kernel Modules

```bash
cat <<EOF | tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
```

---

## Configure sysctl

```bash
tee /etc/sysctl.d/kubernetes.conf <<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
EOF
```

Apply

```bash
sysctl --system
```

Verify

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Expected

```
1
```

---

## Install curl

```bash
apt install curl -y
```

---

## Add Docker GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
```

---

## Add Docker Repository

```bash
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

---

## Install containerd

```bash
apt update -y

apt install -y containerd.io
```

---

## Generate containerd Config

```bash
mkdir -p /etc/containerd

containerd config default | tee /etc/containerd/config.toml
```

---

## Edit Config

```bash
vi /etc/containerd/config.toml
```

Change

```
SystemdCgroup = false
```

to

```
SystemdCgroup = true
```

---

## Restart containerd

```bash
systemctl restart containerd

systemctl status containerd
```

Expected

```
Active: active (running)
```

---

# Phase 3 - Install Kubernetes

Install prerequisites

```bash
apt-get install -y apt-transport-https ca-certificates curl gpg
```

---

Create keyrings

```bash
mkdir -p -m 755 /etc/apt/keyrings
```

---

Add Kubernetes GPG Key

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key \
| gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

---

Add Kubernetes Repository

```bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' \
| tee /etc/apt/sources.list.d/kubernetes.list
```

---

Update

```bash
apt-get update
```

---

Install Kubernetes

```bash
apt-get install -y kubelet kubeadm kubectl
```

---

Enable kubelet

```bash
systemctl enable kubelet
```

---

# Phase 4 - Initialize Cluster

Pull Images

```bash
kubeadm config images pull
```

---

Initialize Cluster

```bash
kubeadm init \
--pod-network-cidr=10.244.0.0/16 \
--ignore-preflight-errors=NumCPU \
--ignore-preflight-errors=Mem
```

---

# Configure kubectl

Create folder

```bash
mkdir -p $HOME/.kube
```

Copy Config

```bash
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```

Permission

```bash
chown $(id -u):$(id -g) $HOME/.kube/config
```

---

# Phase 5 - Install Flannel

```bash
kubectl apply -f https://github.com/coreos/flannel/raw/master/Documentation/kube-flannel.yml
```

---

Verify Nodes

```bash
kubectl get nodes
```

Verify Pods

```bash
kubectl get pods -A
```

---

# Phase 6 - Join Worker

Run on Worker

```bash
kubeadm join <MASTER-IP>:6443 \
--token <TOKEN> \
--discovery-token-ca-cert-hash sha256:<HASH>
```

---

Generate New Join Command

Run on Master

```bash
kubeadm token create --print-join-command
```

---

# Troubleshooting

Check ip_forward

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Should be

```
1
```

Check containerd

```bash
systemctl status containerd
```

Check kubelet

```bash
systemctl status kubelet
```

Check Nodes

```bash
kubectl get nodes
```

Check All Pods

```bash
kubectl get pods -A
```

---

# Memory Flow (Revise Daily)

```text
Root
 ↓
Update
 ↓
Hostname
 ↓
Swap Off
 ↓
Kernel Modules
 ↓
Persist Modules
 ↓
sysctl
 ↓
Apply sysctl
 ↓
Install containerd
 ↓
Generate config.toml
 ↓
SystemdCgroup=true
 ↓
Restart containerd
 ↓
Install kubeadm kubelet kubectl
 ↓
Enable kubelet
 ↓
Pull Images
 ↓
kubeadm init
 ↓
admin.conf
 ↓
.kube/config
 ↓
Flannel
 ↓
Node Ready
 ↓
Join Worker
```

---

# Interview One-Liners

### kubeadm

Creates and bootstraps the Kubernetes control plane.

### kubelet

Node agent responsible for creating and monitoring Pods.

### kubectl

CLI used to communicate with the Kubernetes API Server.

### containerd

Container Runtime that actually runs containers.

### Flannel

CNI plugin that provides Pod-to-Pod networking.

### admin.conf

Contains cluster endpoint, certificates and admin credentials used by kubectl.

### SystemdCgroup=true

Ensures containerd and kubelet use the same cgroup driver.

### pod-network-cidr

IP range from which Pods receive their IP addresses.

### kubeadm join

Registers a worker node with the Kubernetes control plane.
