# Node Affinity

- provides advance capabilities to limit pod placement on different nodes
- more complex

```yaml

apiVersion: v1
kind:  Pod
metadata:
  name: myapp-pod
spec:
  containers: 
  - name: data-processor
    image: data-processor
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:   # the expression field to match on key value. 
          - key: size   # the key
            operator: In # In operator means anything that includes the value
            values:    # the value value field is an array. can have multiple values
            - Large
            - Medium
```

- the following operators are available:
  - In - if any of the key value pair is a match, it is considered a match
  - NotIn - if the key value pair is not on the node, it is considered a match
  - Exists - checks if the label key size exists on the node. this will be considered a match

# Node Affinity Types

- requiredDuringSchedulingIgnoredExecution
  - will not deploy the pod if no match is found
  - changes done to the node will not affect the pod

- preferredDuringSchedulingIgnoredExecution
  - will ignore the affinity rule if no match is found. will place on any available node.
  - changes done to the node will not affect the pod

 - A pod has two states during the lifecycle of affinity: DuringScheduling and DuringExecution

 - DuringScheduling means during the scheduling phase
 - DuringExecution means after the pod has been deployed. what do you do if something changes?

 