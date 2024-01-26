# Secrets

* Set environment variables for a container.
* Provide credentials such as SSH keys or passwords to Pods.
* Allow the kubelet to pull container images from private registries.

## via CLI using a literal
```shell
kubectl create secret <config-map-name> \
 --from-literal=<key>=<value> \
 --from-literal=<key>=<value> 
 
 # Example
 kubectl create secret generic db-user-pass \
    --from-literal=username=admin \
    --from-literal=password='S!B\*d$zDsb='
```

## Converting a plain text to a base64 encoded format
```shell
echo -n "somestring" | base64
```

## Converting a base64 to a text decoded format
```shell
echo -n "c29tZXN0cmluZw==" | base64 --decode
```

## Via CLI using a file
```shell
kubectl create secret <config-map-name> \
 --from-file=<path-to-properties-file>
 
echo -n 'admin' > ./username.txt
echo -n 'S!B\*d$zDsb=' > ./password.txt

# The default key name is the file name. You can optionally set the key name using --from-file=[key=]source. For example:
kubectl create secret generic db-user-pass \
    --from-file=./username.txt \
    --from-file=./password.txt
    
kubectl create secret generic db-user-pass \
    --from-file=username=./username.txt \
    --from-file=password=./password.txt
```

## Via CLI for Docker Registry using a literal
```shell
# This command creates a Secret of type kubernetes.io/dockerconfigjson.
kubectl create secret docker-registry secret-tiger-docker \
  --docker-email=tiger@acme.example \
  --docker-username=tiger \
  --docker-password=pass1234 \
  --docker-server=my-registry.example:5000
```

## Via CLI for Docker Registry using a file
```shell
kubectl create secret docker-registry my-secret --from-file=.dockerconfigjson=path/to/.docker/config.json
```


## Decoding a docker based secret

```shell

# Viewing the contents of a secret
kubectl get secret db-user-pass -o jsonpath='{.data}'

# Decoding a secret
kubectl get secret secret-tiger-docker -o jsonpath='{.data.*}' | base64 -d
```

## Sample 1- Using a secret in a pod

```shell

# DB_HOST
$ echo -n "somehome" | base64
c29tZWhvbWU=

#DB_USER
$ echo -n "someuser" | base64
c29tZXVzZXI=

#DB_PASS
$ echo -n "somepass" | base64
c29tZXBhc3M=

# Create the secret and the pod
k apply -f samples/secrets/sample-1/secrets.yml
k describe secret sample-1-secret
```

```yaml
Name:         sample-1-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
DB_HOST:      8 bytes
DB_PASSWORD:  8 bytes
DB_USER:      8 bytes
```

```shell
# Viewing the data inside the secret
kubectl get secret sample-1-secret -o jsonpath='{.data.*}'

# View how the secrets look like in the pod
k describe po sample-1-secret-pod 

# View the secrets inside the pod
k exec -it sample-1-secret-pod /bin/sh

env | grep USER
USER=someuser

env | grep HOST
HOST=somehome

env | grep PASSWORD
PASSWORD=somepass

```
## Sample 2- Loading all secrets from a secret file

```shell
k apply -f samples/secrets/sample-2/secrets.yml
k exec -it sample-2-secret-pod /bin/sh

env | grep DB_USER
DB_USER=someuser

env | grep DB_HOST
DB_HOST=somehome

env | grep DB_PASSWORD
DB_PASSWORD=somepass
```

---

## Sample 3- Using a volume mount

```shell
k apply -f samples/secrets/sample-3/secrets.yml
k exec -it sample-3-secret-pod /bin/sh

/ # ls /config
DB_HOST      DB_PASSWORD  DB_USER

/ # ls -ltr /config
total 0
lrwxrwxrwx    1 root     root            14 Jan 26 23:23 DB_USER -> ..data/DB_USER
lrwxrwxrwx    1 root     root            18 Jan 26 23:23 DB_PASSWORD -> ..data/DB_PASSWORD
lrwxrwxrwx    1 root     root            14 Jan 26 23:23 DB_HOST -> ..data/DB_HOST


/ # cat /config/DB_HOST
somehome

/ # cat /config/DB_USER
someuser

/ # cat /config/DB_PASSWORD
somepass
```

## Notes

* A secret is only sent to a node if a pod on that node requires it.
* Kubelet stores the secret into a tmpfs so that the secret is not written to disk storage.
* Once the Pod that depends on the secret is deleted, kubelet will delete its local copy of the secret data as well.