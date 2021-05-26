# Probes

https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/


After setting up readiness and liveness we can grep to check
if all works ok.

```
kubectl describe pod nginx | grep -i readiness
```

Get a list of events to find which namespaces had the probes as failed
```
kubectl -n qa get events | grep -i "Liveness probe failed"
```
