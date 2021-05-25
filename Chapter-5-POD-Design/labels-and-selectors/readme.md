# Labels

* Labels are key/value pairs that are attached to objects, such as pods. 
* Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system. Labels
*  can be used to organize and to select subsets of objects. 
*  Labels can be attached to objects at creation time and subsequently added and modified at any time. 
*  Each object can have a set of key/value labels defined. Each Key must be unique for a given object.

# Annotations

* Kubernetes annotations to attach arbitrary non-identifying metadata to objects.

# Selectors

* Via a label selector, the client/user can identify a set of objects

```
selector:
  matchLabels:
    component: redis
  matchExpressions:
    - {key: tier, operator: In, values: [cache]}
    - {key: environment, operator: NotIn, values: [dev]}
```


# Select the pods with a particular label

```
kubectl get all -l env=prod  
kubectl get pods -l <key>=<value>
kubectl get pods -l <key1>=<value1>,<key2>=<value2>
kubectl get pods -l 'key1 in (value1),key2 in (value1)'
kubectl get pods -l 'key1 in (value1, value2)'
kubectl get pods -l 'key1 notin (value1, value2)'
kubectl get pods --selector <key>=<value>
```

> Note: 
> 
> The above commands work with any K8 object.
> 
> When querying, do not add a space between the commas

---

# Rolling Updates & Rollbacks

* Every new deployment - > Creates a - > Rollout - > Creates a Revision
* This feature allows us to rollback to a previous version.

## View the deployment status

```
kubectl rollout status <deployment>
kubectl rollout history <deployment>
```

### Rollout Strategies

* All At Once Roll Out (Recreate) - This is not the default strategy. This brings down all the pods and the nupdates the new pods causing a down time.

* Rolling update (Default) - Updates take place one by one.

#### How to do the updates?

Modify the deployment yaml file, by updating the image to the latest version or a different version of the image and execute

```
kubectl apply -f deployment-definition.yaml
kubectl set image deployment/<object> nginx=nginx:latest
```

View the deployments can be done using 

```
kubectl describe deployment/<object>
```

Process of Rolling updates

* The deployment creates a new replicaset 
* As it brings the pods to ready in the new replica set, it shuts down the pods in the old replica set.
* At this juncture running the following command should show up with 2 replica sets proving the fact that there is an old replica set and a new replica set.

```
kubectl get rs
```

To rollback to the previous version of the deployment

```
kubectl rollback undo deployment/<object>
```

#### References
https://blog.container-solutions.com/kubernetes-deployment-strategies


#### Creating a deployment, verifying rollout status and history

```
kubectl create deployment nginx --image=nginx:1.16
kubectl rollout status deployment/nginx
kubectl rollout history deployment/nginx
kubectl rollout history deployment/nginx --revision=1
kubectl set image deployment nginx <container-name>=nginx:latest --record
kubectl rollout history deployment/nginx
kubectl edit deployments. nginx --record
kubectl rollout history deployment/nginx

```

> Note: 
> 
> The --record saves the history of the command used to update the deployment. 
> 
> The record command can be used when we edite deployments at run-time as well
> 
> The --revision command provides information abot a specific revision

---
