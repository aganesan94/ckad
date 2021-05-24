# Taints and Tolerations

- Node Affinity - Attractions of pod to a node.
- Taints - Applied on *nodes* to repel a set of pods
- Tolerations - Applied to *pods* so they can be scheduled on nodes with matching taints


# Adding a taint

```
kubectl taint node <node-name> key1=value1:NoSchedule
```

NoSchedule - no pod will be schduled to that specific node until the pod has a matching toleration


# Removing a taint

```
kubectl taint node <node-name> key1=value1:NoSchedule-
```

* A taint is set on the master node automatically, so no pods are scheduled on the node.
*  The taint on the masternode/control plan can be removed.