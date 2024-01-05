# Basics

## Pre-requisites
* vi-cheatsheet: https://www.atmos.albany.edu/daes/atmclasses/atm350/vi_cheat_sheet.pdf
* Only k8s docs are permitted: https://kubernetes.io/docs/home/
* Markdown cheatsheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
* CKAD Practice per topic: https://github.com/dgkanatsios/CKAD-exercises/blob/main/a.core_concepts.md
* Arun's CKAD Book: https://github.com/aganesan94/ckad
* Install minikube and kubectl
* Set up kubectl  as alias using the quick reference https://kubernetes.io/docs/reference/kubectl/quick-reference/

---

![Alt Basics]( ./docs/images/basics.png)

## K8s concepts

### PODS

* Smallest object your can create in K8
* Contains one or more containers. Containers cannot be of the same type cannot be run on a pod
* Runs on a Worker Node
* Pods have a one to one relationship with containers
* Pods are transient, they do not store any information persistently unless we specify persistent volumes
* Single pod can have multiple containers which are not of the same type

![Alt Basics]( ./docs/images/pod-basic-definition.png)

```
# Imperative command to run a pod
kubectl run <pod-name> --image <image-name:version>

# Imperative command to run a pod with a --watch
kubectl run <pod-name> --image <image-name:version> --watch

# Imperative commadn to do a quick dry run to check the pod specification
# This can be piped to a file
kubectl run nginx --image=nginx --dry-run=client 

# Getting a list of pods across all namespaces
kubectl get pods --all-namespaces 

# Counting a list of pods across all namespaces
# NOTE: The output is one less than the count provided
kubectl get pods --all-namespaces  | wc -l

# Getting a pods yaml file
kubectl get pod my-pod -o yaml 
 
# Be thorough with all the semantics of pods from this output at all times
# This provide more information of which worker node the pod is deployed or scheduled in
kubectl get pods -o wide

# Delete a pod
kubectl delete pod <pod-name> -n <namespace>

#Force Delete the pod
kubectl delete pod <pod-name> -n <namespace> --force

# Finding the image used to create a  pod
# Note: Word image is in Caps
kubectl describe pod <pod-name> | grep "Image"

# Getting the total number of containers in a pod
kubectl describe pod <pod-name> | grep "Container ID"

# Get the status of the pod
# Look at the last line after describing the pod or look at status
kubectl get pod

# To see why a container is not running, look at the "Events" section
kubectl describe pod <pod-name>

# To fetch the "no of containers running/total containers"  running
# in the pod look at the "status" column using the following command
kubectl get pods 

# Edit a pod
# Change some parameters
# Write to a file
kubectl edit pod <pod-name>
```