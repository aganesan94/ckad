```
alias k=kubectl
```

### Fetch all namespaces
  
```
k get namespaces
k get ns
```

### get all objects from all namespace or a specific object from all namespaces or an pod from a specific namespace

```
k get all --all-namespaces
k get po --all-namespaces
k get po -n <ns-name>
k get svc -n <ns-name>
k get po

k describe po nginx
k delete po nginx
k delete -f po nginx
k delete -f po nginx --force

k describe po nginx

k get po nginx -w
k get po nginx -o wide

k get po --show-labels
k get po -l key1=value1
k get po -L env
k describe po nginx | grep Node-Selectors
k describe po nginx | grep Labels
k describe po nginx | grep Images

kubectl exec -it nginx /bin/sh


kubectl logs busybox -p
kubectl logs busybox -f


```

### Makings sure a pod works on a node
```
k label node minikube nodeName=nginxnode

  nodeSelector:
    nodeName: nginxnode

k describe po nginx | grep Node-Selectors    
k describe po nginx | grep Node-Selectors
```

Imperative Commands

```
kubectl run nginx --image=nginx:1.17.4 --restart=Never --port=80

kubectl run busybox --image=nginx --restart=Never -it -- echo "How are you"

# container-name=imagename:version
kubectl set image pod/nginx nginx=nginx:1.15-alpine

kubectl create deploy webapp --image=nginx:1.17.1

```

```

kubectl rollout pause deploy webapp
kubectl rollout resume deploy webapp
kubectl rollout history deploy webapp
kubectl rollout history deploy webapp --revision=9
kubectl autoscale deploy webapp --min=10 --max=20 --cpu-percent=85


k create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am from job" > hello-job.yaml
k create cronjob date-job --image=busybox --schedule="*/1 * * * *" -- bin/sh -c "date; echo Hello from kubernetes cluster"

```

// emptyDir is the volume that lasts for the life of the pod

kubectl create cm keyvalcfgmap --from-file=config.txt
kubectl create cm keyvalcfgmap --from-literal=config.txt
kubectl create cm envcfgmap --from-env-file=file.env
kubectl create cm cfgvolume --from-literal=var1=val1 --from-literal=var2=val2

  securityContext: # add security context
    runAsUser: 1000
    runAsGroup: 2000