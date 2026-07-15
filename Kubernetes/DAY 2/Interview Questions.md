# Interview Questions & Scenarios

## Conceptual
1. EKS vs ECS vs ECR
2. Why disable Swap?
3. Why containerd instead of Docker?
4. Difference between kubeadm, kubelet and kubectl.
5. Explain kubeadm init.
6. Purpose of admin.conf.
7. Why Flannel?
8. What is the Join Token?
9. Explain the complete kubectl apply flow.
10. Master vs Worker.

## Troubleshooting
- kubeadm init fails
- kubeadm join fails
- Node NotReady
- API Server down
- kubelet stopped
- Flannel missing
- Pods cannot communicate
- Security Group blocks 6443
- Swap enabled
- containerd not running

## Production Scenarios
- Worker Node crashes.
- Control Plane crashes.
- Existing Pods continue but new Pods cannot be scheduled.
- How are Pods recreated after node failure?
- Why are multiple Control Plane nodes used?
- How do Pods communicate across Worker Nodes?
- What happens after kubectl apply?
