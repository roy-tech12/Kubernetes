# 🔥 Services

Service Types
- NodePort

- ClusterIP

- LoadBalancer




# 🛠️ NodePort

makes the pods accessible from outside the cluster on every node's IP. it maps a port on the node to a port on the pod.


- node ports can only be in a valid range : 30,000 - 32,767

- there are three ports involved when providing this service:
  - the node port, service port, and target port
  - the node port is the port on the host/node
  - the service port is the port on the service object (used inside the cluster)
  - the target port is the port of the pod

- the service listens on the node port and forwards the request to the target port and ip address of the pod
- this accomplished through IP tables rules

- the selector for the service links the service object with the pod(s) by matching labels. any pod that contains one of the labels specified is considered match

  - if there is more than 1 pod, it uses a random algorithm to forward requests to that pod and maintains sessionAffinity.

  - if the pods are distributed in multiple nodes, kubernetes automatically creates spans the service object across the cluster.

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
    type: front-end        # must also match this one as well. selector matching uses AND 
```


```bash
kubectl create -f service-definition.yaml # creates the service object.

kubectl get services

kubectl describe service
```

# 🛠️ Cluster IP

- service object that allows a set of pods to communicate with another set of pods (i.e frontend pods to backend pods)
- when the Cluster IP service is created, kubernetes automatically assigns it a virtual IP address from the Service CIDR
- the ports are defined in the spec section of the yaml file
- CoreDNS automatically creates a DNS entry for the Service name, which resolves to the ClusterIP
- the default service type if none is specified under spec type.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: front-end         

spec:
  type: ClusterIP
  ports:
    - targetPort: 80       # pod/container port       
      port: 80             # service port
  selector:
    app: myapp             # label of the pod definition file. links the service to the pod
    type: front-end        # label of the pod defintion file. links the service to the pod
```

# 🛠️ Loadbalancer

Exposes an application to the outside world by provisioning a cloud provider’s external load balancer that forwards traffic into the cluster.

- Builds on top of NodePort and ClusterIP.
  - Cloud Load Balancer → forwards to NodePort → kube-proxy → Pod.
- Supported only on clusters running in environments with load balancer integrations (AWS ELB, Azure LB, GCP LB, etc.).
- Automatically gets an external IP (public VIP).

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp-service

spec:
  type: LoadBalancer
  ports:
    - targetPort: 80       # pod port       
      port: 80             # service port
      nodePort: 30008      # node port

```