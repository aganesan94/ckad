# Networking

* By default k8 comes with "Allow All" as a rule

## Ingress & Egress
---

### UseCase-1
---
User - > Ingress -> K8 (port 80) -> Egress -> Ingress -> API server (port 5000) -> Egress -> Ingress -> DB (port 3306)

* Ingress is incoming traffic from the user
* Egress is outgoing traffic to the server backend.
* Responses sent by the backend to the user do not really matter.

In the above case we will need the following rules

K8 
  - Enable ingress on port 80
  - Enable egress on port 5000
  
API Server  
  - Enable ingress on port 5000
  - Enable egress on port 3306

API Server  
  - Enable ingress on port 3306

### UseCase-2
---
Web pod - > API pod - > DB pod

Allow all enables each pod to interact with the other pod. 
However the web pod should not interact directly with DB pod.

This would mean db pod should allow ingress traffic from API pod

# Solutions supporting network policies

kube-router
calico
romana
weave-net

Note: flannel is not supported

### References

> https://github.com/ahmetb/kubernetes-network-policy-recipes
> https://kubernetes.io/docs/concepts/services-networking/network-policies/

