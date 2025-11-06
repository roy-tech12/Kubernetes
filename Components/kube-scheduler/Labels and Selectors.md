# Labels and Selectors

- In kubernetes labels and selectors can be used to group and filter out objects based on their label.
- labels are metadata set for a given object


``` bash
kubectl get pods --selector app=App1 # displays pods with the label match of app = App1 only
```


```yaml

apiVersion: apps/v1                 
kind: ReplicaSet                    
metadata:                           
  name: myapp-replicaset            
  labels:                           
    app: myapp                    # ReplicaSet Labels  
    type: front-end                 

spec:                              
  template:                        
    metadata:                       
      name: myapp-pod             
      labels:                    # pod object label
        app: nginx
        tier: front-end
    spec:
      containers:
      - name: nginx
        image: nginx

  replicas: 3
  selector:                    
    matchLabels:
      tier: front-end          # match the pod object label      
```