# Kubernetes Commands (In Order)

```bash
apt update -y
hostnamectl set-hostname <hostname>

swapoff -a
# Disable swap in /etc/fstab

modprobe overlay
modprobe br_netfilter

# Configure sysctl
sysctl --system

# Install containerd
systemctl restart containerd

# Install Kubernetes
apt install kubeadm kubelet kubectl -y

systemctl enable kubelet

kubeadm config images pull

kubeadm init --pod-network-cidr=10.244.0.0/16

mkdir -p $HOME/.kube
cp /etc/kubernetes/admin.conf $HOME/.kube/config

kubectl apply -f kube-flannel.yml

kubeadm join ...

kubectl get nodes
kubectl get pods -A
```
