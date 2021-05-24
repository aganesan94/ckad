# Ingress Controller and Ingress Resources

Ingress - Layer 7 architecture which supports SSL and also route mapping

Types of ingress controllers available t o work with K8s include

* ISTIO
* HAPROXY
* NGINX
* GCP
* CONTOUR
* TRAEFIK


Ingress Controller - used to load balance and route traffic
Ingress rources - Routes are defined in resources

* Ingress controllers are not built in.
* NGINX is currently maintained by K8 team to act as a ingress controller

All parameters related to nginx configuration are stored in a config map in K8s.


## Fetch all ingress controllers

```
kubectl get ingress
```

Reference
https://kubernetes.github.io/ingress-nginx/examples/