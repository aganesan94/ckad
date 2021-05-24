# Node Selectors

Consider a use case where you have multiple nodes. Some nodes have higher specifications in terms of memory, cpu and storage
and some have lower. You have a machine learning algorithm which you need to run on a POD with better hardware specifications.

# Labelling the node so the selector of the pod can pick it up

```
kubectl label nodes <node-name> <label-key>=<label-value>
```

```
kubectl label nodes node01 size=large
```

>Note:  If labels on a node change at runtime such that the affinity rules on a pod are no longer met, the pod continues to run on the node. 