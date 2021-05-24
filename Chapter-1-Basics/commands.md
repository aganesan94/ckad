
# Get cluster-info

```
kubectl cluster-info
```

# Get nodes

```
kubectl get nodes
```

# Create using a definition file


# Working with K8 objects

```
kubectl get <object-type> <object-name> -n <namespace>
kubectl describe <object-type> <object-name> -n <namespace>
kubectl delete <object-type> <object-name> -n <namespace>
```



# PODS

```
kubectl run <image-name>
kubectl run <pod-name> --image <image-name:version>
kubectl get pods -o wide

#Force Delete the pod
kubectl delete pod <pod-name> -n <namespace> --force
```

# Replica Set

```
kubectl scale --replicas=<no> -f <rs-defn.yaml>
kubectl scale --replicas=<no> rs <rs-name>
kubectl scale rs 
```

# Exposing Service

```
kubectl expose pod redis --port=6379 --name redis-service -o yaml
kubectl create service nodeport redis --tcp=6379:6379 -node-port=30080 -o yaml --dry-run=client
kubectl create service clusterip redis --tcp=80:80 -o yaml
kubectl create service clusterip my-svc --clusterip="None" -o yaml --dry-run=client 
```

Creates a service and pod with the same name in a single command

```
kubectl run httpd --image=httpd:alpine --port=80 --expose
```

# Running commands with --dry-run

```
--dry-run=client
kubectl run nginx --image nginx --port=8080 --dry-run=client -o yaml
kubectl create deployment webapp --image=kodekloud/webapp-color --dry-run=client -o yaml > d1.yaml
```


#### Creating a Docker Volume

```
docker create volume <volume-name>
```

#### Associating a Docker Volume

```
docker run -v <volume-name-on-host>:<mount-insisde-container> <image-name>
```

###Executing a command in the bash

```
kubectl exec webapp -- cat /log/app.log
```