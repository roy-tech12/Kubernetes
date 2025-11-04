# Imperative

- Explicitly telling kubernetes on how to make the change
- An exmaple of this would be editing the yaml file for an object, and then using the "kubectl replace -f nginx.yaml" command to update the object.
- Imperative approach requires for manual work from the user
- if the object doesn't exist, replace command will fail
- if using the kubectl create command and the object already exist, it will also fail
- in the imperative approach, the administrator must be aware of the configurations and what currently exists


# Declarative

- kubectl apply -f nginx.yaml
    - if the object doesn't exist, it will create it
    - if the object does exist, it will update it based on the configuration file
- requires less work from the administrator

# Imperative Commands

- are useful during the exam to make quick simple changes quickly
- allows you to generate definition templates easily as well


```bash
--dry-run=client 
# add this option to the end of a command. allows you to test a command . will not create the resoruce

-o yaml 
# adding this to the dry run command will create a yaml resource definition on screen. 

kubectl run nginx --image=nginx  --port=8080
# creates a NGINX pod and gives it port 8080

kubectl run ngninx --image=nginx --dry-run=client -o yaml 
# generates a POD manifest yaml file. does not create the pod .

kubectl create deployment --image=nginx nginx
# creates a deployment using the ngninx image

kubectl create deployment --image=nginx nginx --replicas=4 
# creates a deployment with with a replca of 4

kubectl create deployment ngninx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml 
# forwards the output of the yaml file to a file called ngninx-deployment.yaml

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
# creates a cluster ip service called redis-service. automatically use the pod's(redis) labels as selector.

kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
# creates a nodeport service . usues port 30080 . you to definition nodeport, you must generate a yaml first and edit it. 
```

