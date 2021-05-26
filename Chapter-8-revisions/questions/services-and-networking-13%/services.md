# Services

```
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - name: http
      protocol: TCP
      port: 80
      targetPort: 9376
    - name: https
      protocol: TCP
      port: 443
      targetPort: 9377
```

Imperative Commands

```
# Created a service and exposes it as a nodeport
kubectl run nginx --image=nginx:1.17.4 --port=80 --expose

# The above command can be exposed using the following
kubectl run nginx --image=nginx:1.17.4 --port=80
kubectl expose po nginx --type=NodePort --port=80  --target-port=30080 -name nginx-svc

# Creating a service directly
kubectl create service nodeport redis --tcp=6379:6379 -node-port=30080 
kubectl create service clusterip redis --tcp=80:80
kubectl create service clusterip redis --clusterip="None" 

kubectl get svc nginx-svc -o wide


kubectl get svc -l app=my-nginx
```
