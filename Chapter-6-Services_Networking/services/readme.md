# Services

## Create a service
```
kubectl create -f service-definition.yaml
```

## Get Services
```
kubectl get services
```
## Get a specific Service
```
kubect get service <service-name>
```

## Accessing a port outside of the node
```
curl http://<node-ip>:NodePort -v

```
## Accessing a pod using cluster ip or service name
```
curl http://clusterip:port -v
curl http://servicename:port -v

```


## Node Ports

* Has session affinity.
* Uses a Random algorithm for accessing the pods if many pods are mapped to a service in a given node.
* If there are multiple pods, dispersed across multiples nodes, it maps the services across the same NodePort across all the nodes
* Incase of multiple nodes the accessing of the pod will be based on IP of each of the nodes.

>nodePort : The port on the node where external traffic will come in on
> 
>port : The port of this service
> 
>targetPort The target port on the pod(s) to forward traffic to

### Useful Imperative Commands

```
kubectl run nginx --image nginx --port=80 --expose
kubectl create service nodetype <podname> --tcp=<targetPort>:<containerPort>
kubectl create service clusterip <podname> --tcp=<targetPort>:<containerPort>

```
