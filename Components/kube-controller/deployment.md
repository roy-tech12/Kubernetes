# Deployments

A Deployment in Kubernetes is a higher-level abstraction that manages ReplicaSets and Pods. Deployments make it easy to:

- Roll out new versions of an application using rolling updates
- Pause and resume updates when needed
- Perform rollbacks to a previous stable version
- Scale applications up or down seamlessly


```yaml

apiVersion: apps/v1                      # Supported API version
kind: Deployment                         # Type of Object
metadata:                                # Meta Data for Replication controller
  name: myapp-deployment                 # Name of the 
  labels:                                # Labels
    app: myapp                           # customer key value pairs to identify controller
    type: front-end                      # customer key value pairs to identify controller

spec:                                    # Defines whats inside the object you are creating
  template:                              # The contents of pod definition yaml file.
    metadata:                       
      name: myapp-pod             
      labels:                    
        app: nginx
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx

  replicas: 3                           # the number of pods
  selector:
    matchLabels:
      app: nginx

```


# BASIC COMMANDS

```bash
kubectl create -f deployment-definit.yaml    # creates the deployment based on the file

kubectl get deployments                 # displays a list of pods available

kubectl get replicaset                  # displays the replicaset created by the deployment

kubectl get all.                        # display all objects created at once.

kubectl apply -f deployment-definit.yaml  # if the deployment doesnt exist, it creates based on the manifest file. if it does exist, it updates it based on the manifiest file.
```

