Ingress Controller
---
```
minikube addons enable ingress
echo "$(minikube ip) now-what.com" | sudo tee -a /etc/hosts
kubectl expose -f deployment.yaml --port=8080 --type=LoadBalancer
minikube service my-app
kubectl get svc my-app -o yaml
kubectl delete svc my-app
kubectl create -f ingress.yaml
kubectl get ingress my-ingress -o yaml
```
