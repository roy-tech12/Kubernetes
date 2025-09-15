# 🔥  Services

Service Types
- NodePort
- ClusterIP
- LoadBalancer


# NodePort

maps a port on the node to a port on the pod.
- node ports can only be in a valid range : 30,000 - 32,767
- there are three ports involved when providing this service:
  - the node port, service port, and target port
  - the node port is the port on the host/node
  - the service port is the port on the service object
  - the target port is the port of the pod
- the service listens on the node port and forwards the request to the target port and ip address of the pod


```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service

spec:
  type: NodePort
  ports:
    - targetPort: 80       # pod port       
      port: 80             # service port
      nodePort: 30008      # node port
  selector:
    app: myapp             # label of the pod definition file. links the service to the pod
    type: front-end        # label of the pod defintion file. links the service to the pod
```

kubectl create -f service-definition.yaml

kubectl get services

