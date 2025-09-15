# Kubernetes Pods

Containers are encapsulated into a Kubernetes object called a **Pod**.

- Smallest object you can create in Kubernetes
- **1 Pod = 1 container** (in most cases)
  - A single Pod *can* have multiple containers, but usually not of the same kind
  - Helper containers (sidecars) can be deployed within the same Pod
  - Containers in the same Pod can communicate directly via localhost
  - Multi-container Pods are a rare use case
- To scale, you create more Pods — either on the same node or another node in the cluster

# Example Pod Manifest

File: `pod-definition.yml`

```yaml
apiVersion: v1                # API Version
kind: Pod                     # Type of object
metadata:                     # Information about the pod (must match k8s expectations)
  name: myapp-pod             # Pod name
  labels:                     # Key-value pairs (used for selectors, organization)
    app: nginx
    tier: frontend
spec:
  containers:
  - name: nginx
    image: nginx
```
# BASIC COMMANDS

```bash
kubectl create -f pod-definition.yml    # creates the pod based on yaml file.

kubectl get pods                        # displays a list of pods available

kubectl describe pod podname            # displays detailed information regarding a pod

kubectl delete pod podname              # deletes a pod
```