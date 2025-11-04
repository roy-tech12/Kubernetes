# 🔥 Scheduling

- Pod YAML configuration files have a nodeName field that can be used to specify the node to a deploy pod in. If the nodeName is not included, Kubernetes will automatically assign the pod to a node via a scheduling algorithm.
- If there is no scheduler, pods will be stuck in a pending state.


```bash

kubectl get nodes # lists the nodes in kubernetes cluster

kubectl get pods -n kube-system # lists the pods running in the kube-system namespace. scheduler runs in this namespace

```

- to manually assign the kubernetes pod a node, edit the yaml configuration file and use "kubectl replace --force -f config.yaml"
- replace will delete the pod and re-create it based on the configuration file.

```yaml
apiVersion: v1                # API Version
kind: Pod                     # Type of object
metadata:                     # Information about the pod (must match k8s expectations)
  name: myapp-pod             # Pod name
  namespace: dev              # namespace . will use default if not specified.
  labels:                     # Key-value pairs (used for selectors, organization)
    app: nginx
    tier: frontend
spec:
  nodeName: node01            # field to manually select a node to deploy the pod in
  containers:
  - name: nginx
    image: nginx
```