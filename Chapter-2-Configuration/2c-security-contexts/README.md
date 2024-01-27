# Security Contexts

<!-- TOC -->
* [Security Contexts](#security-contexts)
  * [Docker](#docker)
  * [Sample - 1 : Applying security Contexts to the level of the pod](#sample---1--applying-security-contexts-to-the-level-of-the-pod)
  * [Sample - 2: Applying security Contexts to the level of the container](#sample---2-applying-security-contexts-to-the-level-of-the-container)
  * [Sample - 3: Applying security Contexts and adding capabilities for a container](#sample---3-applying-security-contexts-and-adding-capabilities-for-a-container)
<!-- TOC -->

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

```shell
docker run --cap-add MAC_ADMIN ubuntu
docker run --cap-drop MAC_ADMIN ubuntu
docker run --privileged ubuntu
```

Security contexts can be configured at 2 levels

* Level of pod (applies to all containers)
* Level of container
* Security context at the container level overrides the specs at the pod level
* If no security context is specified the pod/container runs as a root user

## Sample - 1 : Applying security Contexts to the level of the pod
```shell
k apply -f samples/sample-1/sc.yml
```

## Sample - 2: Applying security Contexts to the level of the container
```shell
k apply -f samples/sample-2/sc.yml
```

## Sample - 3: Applying security Contexts and adding capabilities for a container
* Capabilities do not work at the POD level and can only work on the container level
```shell
k apply -f samples/sample-3/sc.yml

$ k exec -it sc-sample-3-pod -- whoami
root
```

