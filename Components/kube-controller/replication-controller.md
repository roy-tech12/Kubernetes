# Replication Controller

The replication controller helps run multiple instances of a pod in a kubernetes cluster in order to provide high availability.

- In scenarios where you are deploying a single pod, the controller can ensure a new pod is spun up in the event that the pod fails. 
- It ensures the specified number of pods are running at all times


```yaml

apiVersion: v1                      # Supported API version
kind: ReplicationController         # Type of Object
metadata:                           # Meta Data for Replication controller
  name: myapp-rc                    # Name of the 
  labels:                           # Labels
    app: myapp                      # customer key value pairs to identify controller
    type: front-end                 # customer key value pairs to identify controller

spec:                               # Defines whats inside the object you are creating
  template:                         # The contents of pod definition yaml file.
    metadata:                       
      name: myapp-pod             
      labels:                    
        app: nginx
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx

  replicas: 3                       # the number of pods

```

# BASIC COMMANDS

```bash
kubectl create -f rc-definition.yml   # creates the the replication controller. After the controller is created, it creates the pods based on the definition

kubectl get replicationcontroller     # information about the replication controller. starts with thename of the replication controler

kubectl get pods                      # displays pods created by the replication controller
```


# ReplicaSet

New recommended way to setup replication. Provides similiar functionality to Replication Controller

```yaml

apiVersion: apps/v1                 # Supported API version. Replicaset must use apps/v1
kind: ReplicaSet                    # Type of Object
metadata:                           # Meta Data for Replication controller
  name: myapp-replicaset            # Name of the 
  labels:                           # Labels
    app: myapp                      # customer key value pairs to identify controller
    type: front-end                 # customer key value pairs to identify controller

spec:                               # Defines whats inside the object you are creating
  template:                         # The contents of pod definition yaml file.
    metadata:                       
      name: myapp-pod             
      labels:                    
        app: nginx
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx

  replicas: 3
  selector:                          # Diff between replication controller and replicaset. Required by Replica Set, optional for Controllers. Tells it what     pods fall under it. If there are pods created that match the selector that were created before replicaset, those will also be considered.
    matchLabels:
      type: front-end                # All Pods that container the "type: front-end" label will match. This is why setting labels is important.
```

# BASIC COMMANDS

```bash
kubectl create -f replicaset-definition.yml   # creates the the replication controller. After the controller is created, it creates the pods based on the definition

kubectl get replicaset                        # information about the replication controller

kubectl get pods                              # displays pods created by the replication controller

kubectl replace -f replicaset-definition.yml  # replicaset object is updated in etcd but the existing pods keep runningw ith old image. new pods would use the new image. you must delete the pod.

kubectl scale --replicas=6 -f replicaset-definition.yml   # scales the replicas to 6 but does not update the file itself. will stil be 3.

kubectl delete replicaset myapp-replicaset.   # deletes a replicaset
```

