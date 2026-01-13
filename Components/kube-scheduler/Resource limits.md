# Resources Limits


- Resource requests is the minimum requirement for a pod when being deployed on a node
- Scheduler uses this number to determine what nodes have sufficient resources to support the pod
- set inside the pod yaml config file
- if there is no pods with sufficient resources available, pod will stay in the pending state
  - kubectl pod describe command will show Insufficent CPU as the reason.


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
    ports:
      - containerPort: 8080
    resources:
      requests:
        memory: "4Gi" # Min ammount of memory requested. Scheduler looks for nodes that has the ammount free.
        cpu: 2 # Min amount of cpu requested. Scheduler looks for nodes that has the ammount free.
      limits:
        memory: "8Gi" # Max ammount of memory it can consume on the node
        cpu: 2 # Max ammount of CPU it can consume
```


- When a pod tries to exceed the recourses beyond the specified limit:
  - for CPU, it throttles
  - for memory, it can go over but if it does it constantly, it will be terminated with a Out of Memory message (OOM)

By default, pods do not have limits or requests setting set.
  - you not need to have both set
  - if no request is set , but a limit is set, then the pod is automatically configured with the limit amount as the request
  - if no limit is set and request is set, pods are guaranteed the request amount but are not limited. 
  - you can have different settings for multiple containers within a single pod.


# LimitRange

- allows you to set to limits on pods that have not been configured with limit/requests in the pod definition file.
- done at the namespace level

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
  - default:
      cpu: 500m
    defaultRequests:
      cpu: 500m
    max:
      cpu: "1"
    min:
      cpu: 100m
    type: Container
```

- enforce when a pod is created
- if changes are made to a limit range, it does NOT affect existing pods.


