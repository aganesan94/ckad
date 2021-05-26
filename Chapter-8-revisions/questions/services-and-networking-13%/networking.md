# Network Policies

https://kubernetes.io/docs/concepts/services-networking/network-policies/

## Denies All Ingress traffic

```
podSelector: {}
policyTypes:
- Ingress
```

## Allows All Ingress traffic 

```
podSelector: {}
policyTypes:
- Ingress
ingress:
- {}
```

## Denies All Egress traffic

```
podSelector: {}
policyTypes:
- Egress
```

## Allows All Ingress traffic 

```
podSelector: {}
policyTypes:
- Egress
egress:
- {}
```
## Targeting a range of ports

```
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.0/24
    ports:
    - protocol: TCP
      port: 32000
      endPort: 32768

```

### A generic Network policy which ensures the following

DB Pod can be accessed only if the following are trued

#### Ingress

* From a given IP block 
* with namespace labels
* with pod labels
* port 6379

#### Ingress

* on a particular port

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - ipBlock:
        cidr: 172.17.0.0/16
        except:
        - 172.17.1.0/24
    - namespaceSelector:
        matchLabels:
          project: myproject
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 6379
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.0/24
    ports:
    - protocol: TCP
      port: 5978

```