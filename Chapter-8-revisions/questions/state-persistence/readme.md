# Storage Persistence

## Creating a PV, PVC, Pod

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  containers:
  - args:
    - sh
    - -c
    - sleep 3600
    image: busybox:latest
    name: busybox
    volumeMounts:
    - name: my-vol
      mountPath: /etc/foo
  volumes:
  - name: my-vol
    persistentVolumeClaim:
      claimName: my-pvc 

```

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: myvolume
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Retain
  storageClassName: normal
  hostPath:
    path: /etc/foo

```

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  storageClassName: normal
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 4Gi

```


## Creating a volume with emptydir. Emptydir stays for the lifetime of the pod.

```
volume:
- name:
  emptyDir: {}
```

## Creating a mount with readonly inside the pod

```
volumeMounts:
- name: all-in-one
  mountPath: "/projected-volume"
  readOnly: true
```



