# Resources Limits


- Resource requests is the minimum requirement for a pod when being deployed on a node
- Scheduler uses this number to determine what nodes have sufficient resources to support the pod
- set inside the pod yaml config file


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
  containers:
  - name: nginx
    image: nginx

    resources:
      reqeuests:
        memory: "4Gi"
        cpu: 2
```