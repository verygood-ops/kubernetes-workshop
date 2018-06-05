
```
kubectl apply -f deployment-v1.yaml
kubectl apply -f service.yaml
minikube service nginx
kubectl apply -f deployment-v2.yaml
kubectl edit nginx
kubectl edit service/nginx
```

```
helm install --name cert-manager stable/cert-manager
```