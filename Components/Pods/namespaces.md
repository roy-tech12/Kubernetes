# Namespace

a logical partition within a Kubernetes cluster
- used to separate and organize resources
- provides multi-tenancy, resource isolation, and simpler access control
- by default, resources exist in the **default** namespace if none is specified.

each namespace can be also be given Resource Limits. 

resources in different namespaces can communicate with each other. they must append the name of the namespace to the service they are trying to communicate with.
- pods within the same namespace do not need to append the namespace name to the service. 

# Built-in Namespaces

- default → where resources go if no namespace is specified.
- kube-system → system pods & services (DNS, controllers, kube-proxy, etc.).
- kube-public → publicly readable data (e.g., cluster info ConfigMap).
- kube-node-lease → holds node lease objects for faster node heartbeat checks.

# Across Namespaces

- services in a particular namespace can communicate with a service in another namespace by appending the namespace to the name of the service
- db-device.dev.svc.cluster.local
    - dev is the namespace name
    - cluster.local is the default domain name
    - svc is the sub-domain

# Namespace

```yaml

apiVersion: v1
kind: Namespace
metadata:
  namespace: dev
```

# Namespace Commands

```bash

# List pods in the kube-system namespace
kubectl get pods --namespace=kube-system

# Create namespace
kubectl create namespace dev

# View details
kubectl describe namespace dev

# Create a pod in another namespace
kubectl create -f pod-definition.yml --namespace=dev

# Run a pod in a namespace
kubectl run nginx --image=nginx -n dev

# Switch namespace for kubectl (using context)
kubectl config set-context --current --namespace=dev

# Delete a namespace (deletes ALL resources inside!)
kubectl delete ns dev

# retrieves a list of pods across all namespaces
kubectl get pods --all-namespace

```


# Resource Quota

- namespace allow you to limit the amount of resources they consume via ResourceQuota

```yaml

apiVersion: 1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi
```

