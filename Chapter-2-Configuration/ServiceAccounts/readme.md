# Accounts

There are 2 types of accounts in K8s

- User (admin/Developer)
- Service (Jenkins, Prometheus)

* A service account provides an identity for processes that run in a Pod.
* All service accounts create a token, is stored as a secret and is used as for authentication. This can be viewed by describing the secret


```
kubectl create serviceaccount <service-account>
```

* This token can be used as a bearer token to work with the APIs in K8s

```
curl <url> -insecure --header "Authorization Bearer ..."

```

* When describing a pod, a volumes is mounted for the token used to create the pod as a resource on that namespace  which refers to a secret.
* Within the pod the volume is mounted on to a path to provide access to the secrets.