## How to deploy a simple nginx app

1. Create deployment
```
kubectl create deployment nginx --image=nginx
```
2. Get deployment description
```
kubectl get deployment nginx -o yaml > resumen.yaml
```

3. Update the yaml file using the nex code adding the ports 80 TCP
```yaml
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        ports:
        - containerPort: 80
          protocol: TCP
```

4. Deploy the new configuration
```
kubectl replace -f resumen.yaml
```

5. Expose the deployment (only visible inside the cluster)
```
kubectl expose deployment/nginx
```
6. get the ip of the service created by the expose. (You can curl this IP inside a cluster node)
```
kubectl get svc
```
7. scale up or down the replicas of the deployment
```
kubectl scale deployment nginx --replicas=3
kubectl scale deployment nginx --replicas=2
kubectl scale deployment nginx --replicas=0
```

8. Expose deployment to the public

8.1 delete the current service

```
kubectl delete svc nginx
```

8.2 create a new expose with `loadbalancer` type


```
kubectl expose deployment nginx --type=LoadBalancer
```

9. get the public ip to call from a public browser
```
kubectl get svc
```

10. Use the EXTERNAL_IP on your browser you should see

        Welcome to nginx!
        ...
