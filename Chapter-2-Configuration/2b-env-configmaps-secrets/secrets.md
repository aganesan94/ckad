# Secrets

* Set environment variables for a container.
* Provide credentials such as SSH keys or passwords to Pods.
* Allow the kubelet to pull container images from private registries.

## via CLI using a literal
```shell
kubectl create secret <config-map-name> \
 --from-literal=<key>=<value> \
 --from-literal=<key>=<value> 
```
## Via CLI using a file
```shell
kubectl create secret <config-map-name> \
 --from-file=<path-to-properties-file>
```

## Via CLI for Docker Registry using a literal
```shell
kubectl create secret docker-registry my-secret --docker-server=DOCKER_REGISTRY_SERVER --docker-username=DOCKER_USER --docker-password=DOCKER_PASSWORD --docker-email=DOCKER_EMAIL
```

## Via CLI for Docker Registry using a file
```shell
kubectl create secret docker-registry my-secret --from-file=.dockerconfigjson=path/to/.docker/config.json
```