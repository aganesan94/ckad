# Storage and Persistence

## Docker Storage

Docker based container storage can be achieved in 2 ways

* Storage Drivers
* Volume Drivers

### Storage Drivers

* Docker by default stores files in the **/var/lib/docker** folder on the host machine
  
```
$ ls -l /var/lib/docker

/aufs
/images
/containers
/volumes

```
- images - Stores all the images
- containers - Stores all the containers 
- volumes - Stores all the volumes which are created

* Docker works on the basis of layers
* Consider a base docker image 

```
 FROM node:12-alpine
 RUN apk add --no-cache python g++ make
 WORKDIR /app
 COPY . .
 RUN yarn install --production
 CMD ["node", "src/index.js"]
```

The above Dockerfile creates 6 layers, each instruction set is a layer. So if you create another Dockerfile which has the first 2 lines to be common the docker cache will generate the 3rd layer from the 2nd layer

```
 FROM node:12-alpine
 RUN apk add --no-cache python g++ make
  CMD ["node", "src/index.js"]
```

* Once built the layers are not modifiable.
* Modification can occur only on adding of layers.
* When a container in spawned from an image, the image is a read only layer. The container is the only writeable layer. 
* Containers are transient, anything written on to them is lost.
* Containers are still a read/write layer.
* The fact that containers are transient makes it not suitable for using it for persistent data such as databases.Docker addresses this deficiency using **volumes.**

#### Creating a Docker Volume

```
docker create volume <volume-name>
```

#### Associating a Docker Volume

```
docker run -v <volume-name-on-host>:<mount-insisde-container> <image-name>
```

Note:

-  Even if the Docker volume is not created by using the **docker create volume** command the **docker run** command will create it on the fly if one does not exist. This is called the **Volume mount**
  
-  If a directory already exists in the host, it can be mounted as a volume by using the **docker run -v** command. This is call the **Bind mount**

- The preferred way to use docker run is to use the **--mount** option instead of the **-v** option

```
docker run \
-- mount type=bind \
        source=<host-path> \
        target=<container-path> <image-name>
```

The following storage drivers are currently supported by Docker

* AUFS
* ZFS
* BTRFS
* DeviceMapper
* Overlay
* Overlay2

* Storage driver is automatically chosen based on the OS
* Storage Drivers are responsible for spawning and managing images and containers.
---

### Volume Drivers

* Volume Drivers handle volumes
* Volumes are created because pods are transient. When pods are removed or deleted the data residing in the pods is deleted.
* By default the volume plugin used is local.
* The volumes by default are stored in **/var/lib/docker**
* Volumes can be created using the following command
```
docker run -it \
--name mysql \
--volume-driver <volume-driver> \
--mount \
src=<host-path> \
target=<volume-path> \
mysql
```

## Peristent Volumes

* Can be provisioned by administrator
* Can be dynamically provisioned thru storage classes.
  

## Peristent Volume Claim

* A PersistentVolumeClaim (PVC) is a request for storage by a user. 
* It is similar to a Pod. 
* Pods consume node resources and PVCs consume PV resources. 
* Pods can request specific levels of resources (CPU and Memory). 
* Claims can request specific size and access modes

Three types of PVC

* Static - User creates PVs 
* Dynamic - Cluster dynamically provisions a claim
* Binding - User created or dynamically created, control loop in master watches the new pvcs finds a match if possible.

Use cases around the pvc, pv and pods

- If a pod is associated to the PVC, any attempt to delete the PVC, the PVC will be stuck in *terminating* state. On deleting the pod PVC will be deleted.
 
- If a PVC is associated to the PV, and the PVC is deleted and the PV is in *persistentVolumeClaimMode=Retain*, then the PV has to be manually deleted.If it is in *Recycle* it will be automatically deleted.

- On successful deletion of PVC, and if the PV has *persistentVolumeClaimMode=Retain*, it will be in status Released

- The PVC is associated to the PV only if a pod is scheduled and not just by finding a match provided the VolumeBindingMode of StorageClass is set to *WaitForFirstConsumer*
- 
```
kubectl get pv
kubectl get pvc
kubectl get storageclass
```

## Storage class

- Required if used with cloud providers
- Determines how containers are run using docker.
- local-storage does not allow for dynamic provisioning.
- Dynamic provisioning is done using storage classes and does not require a pv definition