# Taints and Tolerations

- Restricts what pods can be scheduled on a node
- Taints are set on nodes, tolerations are set on pods


``` bash

kubectl taint nodes node-name key=value:taint-effect

```

- the taint-effect field defines what happens to the pod if it does not match.
- there are several options for taint-effect:
  - NoSchedule
  - PreferNoSchedule
  - NoExecute: means new pods will not be scheduled. existing pods will be evicted

- Taints are set on nodes and Tolerations are set on Pods

Adding toleration to a pod via a field in the spec field of a pod configuration file:
  - the values for the tolerations field on the pod are obtained from the configured values on the nodes.
  - they must match

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  spec:
    containers:
    - name: nginx-controller
      image: nginx
    tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```

- if a node has no restriction, it will accept any pods regardless of its toleration

```bash
kubectl describe node kubemaster | grep  Taints # by default master node will not accept any pods on it. master node is reserved for management plane.
```