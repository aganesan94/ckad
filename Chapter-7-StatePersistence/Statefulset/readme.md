## StatefulSets

### Need for a stateful set

Consider a usecase of MYSQL DB replication. It has the following sequence of events to set up a MYSQL cluster

* We set up MYSQL Master with 2 slaves for fault tolerance
* All writes will be done on the master
* All reads will be done on the slave

Procedure

* Set up master
* Set up slave
* Clone master to slave
* Enable continuous replication from master to slave
* Clone data from Slave 1 to Slave 2
* Enable continuous replication from master toslave 2
* Configure Slave 1 and Slave 2 to point to master host

The above use case can be done using K8 deployments. Deployments come with the following deficiencies

* Pods can be deleted
* If delete it is hard to understand which one is master and which one is slave
* Pods may crash
* Does not guarantee order of scaling

To overcome this issue we use StatefulSets. Statefulsets have the following advantages

* Creation is ordered
* Scaling up and down is ordered
* Rollback is ordered
* Maintains identity for pods

Each pod in the set will have a stable unique name for example

- mysql-0
- mysql-1
- mysql-2

> Note: refer:statefulset-mysql.yaml

We need a service which gives us a DNS entry to reach each pod.
So we need a headsless service. When a headless-service is created the following
DNS record gets created
podname.headless-servicename.namesace.svc.cluster-domain

Adding the following in the headless-service.yaml creates a service of the above format

```
clusterIP: None
```

and

in the pod definition the following assuming the type is still **Deployment**

```
subdomain: <name-of-headless-service>
hostname: mysql-pod
```

Doing this will accomplish the same dns entry for all the pods in the following format 

> mysql-0: mysql-pod.mysql-h.default.svc.cluster.local
> 
> mysql-1: mysql-pod.mysql-h.default.svc.cluster.local
> 
> mysql-2: mysql-pod.mysql-h.default.svc.cluster.local

This can be overcome by modifying the **kind: StatefulSet** and adding a serviceName
in the spec

```
serviceName: <same-as-headless-service>
```


* By default a PVC is shared in a StatefulSet. Not all storage options do not support this option
*  This can be achieved using a volumeClaimTemplates section under the stateful set definition which has all the information of hte PersistentVolumeClaim. This definition creates a PV and a PVC per replica or per pod. it is an array