# Logs
```
kubectl logs -f <pod-name>
kubectl logs -f <pod-name> <container-name>
```

> Note:  The above statements do not have the object

# Monitoring

* Monitoring k8s was started by Heapster which was deprecated and followed on by MetricsServer
* It is an in memory monitoring solution
* Kubelet receives API instructions from the master server, it contains C-Advisor which in turn exposes metrics from pods to Metrics Server

```
minikube addons enable metrics-server
```

Once installed the following command provides the info on no of cpu/memory available/used.

```
kubectl top node
kubectl top pods
```

