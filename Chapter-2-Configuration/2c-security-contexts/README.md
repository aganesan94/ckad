# Security Contexts

## Docker
* Docker containers run so that they can only see their processes only
* root runs a PID of 1 inside the container
* Docker can be made to run a command with a specific user id using the following

```shell
docker run --user=1000 ubuntu sleep 3000
```

* Alternatively this can be set in the dockerfile

```
FROM ubuntu
USER 1000
```

* Docker capabilities can be modified using the following commands

```
docker run --cap-add MAC_ADMIN ubuntu
docker run --cap-drop MAC_ADMIN ubuntu
docker run --privileged ubuntu
```

Security contexts can be configured at 2 levels

* Level of pod (applies to all containers)
* Level of container
* Execute the following command

```
kubectl exec <pod-name> -- whoami
```

* Security context at the container level overrides the specs at the pod level