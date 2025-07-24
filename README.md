# Minikube & Kubernetes Quickstart Guide

This guide helps you get started with Minikube for local Kubernetes cluster development. It covers installation, cluster management, kubectl essentials, deploying applications, debugging, and working with config files.

---

## 🧰 Installation

Install Minikube and required tools using Homebrew (macOS):

```bash
brew update
brew install minikube
brew install kubectl
```

Check installation:

```bash
minikube version
kubectl version --client
```

---

## 🚀 Start a Minikube Cluster

Create a Kubernetes cluster using Docker as the driver:

```bash
minikube start --driver=docker
```

Verify the cluster status:

```bash
kubectl get nodes
minikube status
kubectl version
```

---

## 🧹 Delete & Debug Cluster

To delete the cluster:

```bash
minikube delete
```

To start the cluster in debug mode:

```bash
minikube start --driver=docker --v=7 --alsologtostderr
```

Check cluster status again:

```bash
minikube status
```

---

## 📋 Basic `kubectl` Commands

Get all resources in the current namespace:

```bash
kubectl get all
```

List nodes, pods, services:

```bash
kubectl get nodes
kubectl get pods
kubectl get pods --watch              # Watch pod status updates
kubectl get pods -o wide              # Detailed view (IP, node, etc.)
kubectl get svc                       # Same as kubectl get services
```

Get other resource types:

```bash
kubectl get secrets
kubectl get configmaps
```

---

## 🚢 Deployments

Create a deployment:

```bash
kubectl create deployment nginx-depl --image=nginx
```

Check deployment, replicaset, and pods:

```bash
kubectl get deployments
kubectl get replicaset
kubectl get pods
```

View YAML definition stored in etcd:

```bash
kubectl get deployment nginx-depl -o yaml
```

Edit deployment in-place:

```bash
kubectl edit deployment nginx-depl
```

Delete a deployment:

```bash
kubectl delete deployment nginx-depl
```

---

## 🐞 Debugging Pods

View pod logs:

```bash
kubectl logs <pod-name>
```

Describe pod status and events:

```bash
kubectl describe pod <pod-name>
```

Execute shell inside a container (if bash is available):

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

---

## 🍃 MongoDB Example Deployment

Create MongoDB deployment:

```bash
kubectl create deployment mongo-depl --image=mongo
```

Debug MongoDB pod:

```bash
kubectl get pods
kubectl logs <mongo-pod-name>
kubectl describe pod <mongo-pod-name>
kubectl exec -it <mongo-pod-name> -- /bin/bash
```

Delete the MongoDB deployment:

```bash
kubectl delete deployment mongo-depl
```

---

## ⚙️ Working with YAML Config Files

Create/edit a config file:

```bash
vim nginx-deployment.yaml
```

Apply (create/update) resources from a file:

```bash
kubectl apply -f nginx-deployment.yaml
```

Delete resources from a file:

```bash
kubectl delete -f nginx-deployment.yaml
```

---

## 📊 Metrics (Optional: metrics-server must be installed)

Get CPU & memory usage:

```bash
kubectl top nodes
kubectl top pods
```

---

## 🌐 Services

Describe a service:

```bash
kubectl describe service nginx-service
```

Expose a service and access it via browser:

```bash
minikube service <service-name>
```

---

## 🔐 Creating Secrets

Create a base64-encoded secret:

```bash
echo -n 'your-username' | base64
echo -n 'your-password' | base64
```

Create a secret via YAML or CLI.

---

## 🧱 Namespaces

View all namespaces:

```bash
kubectl get namespaces
```

Create a new namespace:

```bash
kubectl create namespace my-namespace
```

List non-namespaced API resources:

```bash
kubectl api-resources --namespaced=false
```

---

## 🧼 Cleanup

Delete a pod:

```bash
kubectl delete pod <pod-name>
```

> Note: If the pod is managed by a deployment, it will be automatically recreated.

---

## 📎 Tips

- Use `kubectl explain <resource>` to get documentation on any resource.
- Use `--namespace=<name>` to target a specific namespace.
- You can alias `kubectl` to `k` for speed:
  ```bash
  alias k=kubectl
  ```

---

## ✅ Next Steps

- Install [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
- Learn `kubectl port-forward`, `kubectl rollout`, and Helm for advanced use
- Practice writing your own YAML configs for Deployments, Services, ConfigMaps, and Ingress
