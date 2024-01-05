# Replica Sets

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

> Note: A ReplicaSet ensures that a specified number of pod replicas are running at any given time. However, a Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features

--- 

- ReplicateSet requires a selector but ReplicationController. ReplicateSet can manage pods not created as a part of the template as well.

Replica Sets can be updated in 2 ways

### 1. Replica definition file was used, using the replace

```
kubectl replace -f <rs-defn.yaml>
```


### 2. Replica definition file was used, using the scale

```
kubectl scale --replicas=<no> -f <rs-defn.yaml>
```

### 3. Already deployed replicaset

```
kubectl scale --replicas=<no> rs <rs-name>
```