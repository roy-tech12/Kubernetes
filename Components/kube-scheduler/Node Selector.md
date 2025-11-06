# 🔥 Node Selectors

- You can specify which nodes you want a particular pod to be deployed in by using Node Selectors
- node selectors on a pod match and identify the labels on a node
- the node must be labeled before creating the pod

```bash
kubectl label nodes nodename1 labelkey=keyvalue
```

```yaml
apiVersion:
kind: Pod
metatadata: 
  name: myapp-pod
spec:
  containers:
  - name: data-processor
    image: data-processor
  nodeSelector:  # node selector field
    size: Large  # label that matches on the node
```



