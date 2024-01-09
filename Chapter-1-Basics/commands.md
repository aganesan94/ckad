


# Create using a definition file


# Working with K8 objects

```
kubectl get <object-type> <object-name> -n <namespace>
kubectl describe <object-type> <object-name> -n <namespace>
kubectl delete <object-type> <object-name> -n <namespace>
```





# Replica Set

```
kubectl scale --replicas=<no> -f <rs-defn.yaml>
kubectl scale --replicas=<no> rs <rs-name>
kubectl scale rs 
```

# Exposing Service

```

```



```

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