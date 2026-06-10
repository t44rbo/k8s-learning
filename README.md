# Kubernetes Learning Stack

Production-ready Kubernetes manifests deployed on a real VPS using k3s.

## Stack

- **k3s** — lightweight Kubernetes on Ubuntu 24.04 VPS
- **Nginx** — main deployment with 3 replicas
- **Traefik** — Ingress Controller (built-in k3s)
- **whoami** — routing demo service

## Concepts Covered

- Deployment, ReplicaSet, Pod lifecycle
- Service types: ClusterIP, NodePort
- ConfigMap and Secret management
- Ingress routing by path
- Self-healing and horizontal scaling

## Repository Structure

| File | Description |
|------|-------------|
| `nginx-deployment.yaml` | Main deployment, 3 replicas |
| `nginx-service.yaml` | NodePort service |
| `nginx-configmap.yaml` | App configuration |
| `nginx-secret.yaml` | Sensitive data (values replaced) |
| `nginx-ingress.yaml` | Ingress routing rules |
| `whoami-deployment.yaml` | Second service + routing demo |

## How to Run

```bash
# Install k3s
curl -sfL https://get.k3s.io | sh -

# Fix kubeconfig permissions
sudo chmod 644 /etc/rancher/k3s/k3s.yaml

# Deploy
kubectl apply -f nginx-configmap.yaml
kubectl apply -f nginx-secret.yaml
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
kubectl apply -f whoami-deployment.yaml
kubectl apply -f nginx-ingress.yaml

# Verify
kubectl get pods
kubectl get ingress
```

## Routing

| Path | Service |
|------|---------|
| `/` | nginx |
| `/whoami` | whoami |
