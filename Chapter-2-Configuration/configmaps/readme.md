Config Maps: Allow you to manage configuration data centrally.

Creating using command line

```
kubectl create configmap <config-map-name> \
 --from-literal=<key>=<value> \
 --from-literal=<key>=<value> 
```

```
kubectl create configmap <config-map-name> \
 --from-file=<path-to-properties-file>
```