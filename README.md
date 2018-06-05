##ClusterIP

```
kubectl apply -f cluster_ip.yaml
kubectl port-forward deployment/my-app 8080 8080
```

## NodePort

```
kubectl apply -f node_port.yaml
minikube service my-nodeport-service
```



