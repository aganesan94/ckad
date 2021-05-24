# Editing Pods

#### The only entries which can be edited in the pod definition when the pod is running are as follows


* spec.containers[*].image
* spec.initContainers[*].image
* spec.activeDeadlineSeconds
* spec.tolerations


#### Editing a pod



##### Option 1:

```
kubectl edit pod <pod-name>
```

The above command creates a file in the */tmp/<somefile>.yaml*

###### Delete the existing pod
```
kubectl delete pod <pod-name>
```

###### Create the pod using the 

```
kubectl create -f /tmp/<somefile>.yaml
```

##### Option 2:

```
kubectl get pod <pod-name> -o yaml > <file-name>.yaml
```

###### Delete the existing pod
```
kubectl delete pod <pod-name>
```

###### Create the pod using the 

```
kubectl create -f <somefile>.yaml
```
