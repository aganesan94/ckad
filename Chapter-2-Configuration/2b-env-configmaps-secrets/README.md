# Environment, Configmaps and Secrets

## Environment Variables

### Setting via Docker
```shell
# Set environment variables via docker
docker run -e key=val <image-name>
```
### Setting via K8s
![Alt Basics](./docs/images/env.png)
---

## Config Maps

* Allows for environment variable reuse
*  2 stages
  * Stage 1: Create a configmap
  * Stage 2: Use a file

### via CLI using a literal
```
kubectl create configmap <config-map-name> \
 --from-literal=<key>=<value> \
 --from-literal=<key>=<value> 
```
### Via CLI using a file 
```
kubectl create configmap <config-map-name> \
 --from-file=<path-to-properties-file>
```

### Via Declaration

* Save the below snippet into a file
* Run the following via 

#### Sample 1

##### Commands
```shell
kubectl create -f samples/configmaps/1.yml
# Analysis
kubectl get po configmap-demo-pod
kubectl get cm game-demo

# Notice how the key value parameters in cm are stored
kubectl describe cm game-demo
```
##### What translates to what?
![Alt Basics](./docs/images/cm-desc.png)

##### How to use it in the pod?

```shell
# Shell into the pod
k exec -it configmap-demo-pod /bin/sh
```

```shell
# cat the following files to view the key value pairs
# which are mounted via a volume mount
# config maps in this case are available via a volume mount
# and how they are mounted
ls /config/
cat /config/game.properties
cat /config/user-interface.properties
ls /config/..data/

# The application can now read these files and load
# the environment variables 
# In case of this property, the key and value are directly defined
env | grep PLAYER_INITIAL_LIVES
# In case of this property, the key and value are defined but value contains the file name
# as opposed to the contents of the file.
env | grep UI_PROPERTIES_FILE_NAME
```

#### Sample 2