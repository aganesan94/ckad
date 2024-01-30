# Accounts

There are 2 types of accounts in K8s

- User (admin/Developer)
- Service (Jenkins, Prometheus)

* A service account provides an identity for processes that run in a Pod.
* Create a service account separately, a token separately
* Copy the token which you can use to authenticate with the pod being associated to the SA


```shell
# Create a service account
k create serviceaccount sample-sa

# Create a token, not the token name is same as the service account
# The output of this command can be used to authenticate to 
k create token sample-sa

# Manually creating a token using 
k create -f samples/sample-1/secret.yml

k describe sa sample-sa
```

```yaml
Name:                sample-sa
Namespace:           default
Labels:              <none>
Annotations:         <none>
Image pull secrets:  <none>
Mountable secrets:   <none>
Tokens:              sample-sa-token
Events:              <none>
```

```shell
k describe secrets sample-sa-token
```

```yaml
Name:         sample-sa-token
Namespace:    default
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: sample-sa
              kubernetes.io/service-account.uid: 010ccd53-9863-47d9-93c5-7ffb6f3896df

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1111 bytes
namespace:  7 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImhVN1RUcTg0aUNyOE5LUkFJOGVkTm4tdlNiN0pWWU83dktWdnlDVlA3cDAifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6InNhbXBsZS1zYS10b2tlbiIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJzYW1wbGUtc2EiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIwMTBjY2Q1My05ODYzLTQ3ZDktOTNjNS03ZmZiNmYzODk2ZGYiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpzYW1wbGUtc2EifQ.rvpVsRmrkcq6KODDREK8p_c3Ify-JKWZqhraCkOZcGoHZmfnGAChz0XMXsICgzJmPQ8m9r6t1YZSmu478BNRc6lPKY0i3sQM691VipmulmkyAuT0JLzAtjxfqkfRL90dOiZe0BuPYNZeU09z9aHeYx_XFP7f6x9_ImFvCYGy9EWOY_T9xCJ_MMMlvWizbU74TEcjcS1ueOwpUZaJL_MdQU4crr7fBOJ-FW9m8jeE-xBBU6-2ANe43ijauvNtER8ATBoa0f7yInGLLH5O_Uw6hSCNaR4lrVEJJ7c5fnzR5WuBqzeHoe9CqTEbBSdCgzOvsDY7ipDwEPucKPu40qV_Tg
```

```shell
curl <url> -insecure --header "Authorization Bearer ..."
```

* When describing a pod, a volumes is mounted for the token used to create the pod as a resource on that namespace  which refers to a secret.
* Within the pod the volume is mounted on to a path to provide access to the secrets.