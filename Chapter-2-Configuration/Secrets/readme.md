# Secrets

Used to store information which is confidential


Creating using command line

```
kubectl create secret <secret-name> \
 --from-literal=<key>=<value> \
 --from-literal=<key>=<value> 
```

```
kubectl create secret <secret-name> \
 --from-file=<path-to-properties-file>
```

Converting Secrets from plain text to encrypted format can be done using

> Encoding: echo -n "secret-to-store" | base64
> 
> Decoding: echo -n "secret-to-store" | base64 --decode


Viewing secrets can be done using the following command

```
kubectl get secret <secret-name> -o yaml
```

As such secrets are not safe even if encoded in base64. Refer https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/