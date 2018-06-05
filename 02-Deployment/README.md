[Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
---

```
kubectl apply -f deployment.yaml
kubectl rollout status -f deployment.yaml
kubectl port-forward deployment/my-app 8080 8080
kubectl set image deployment/my-app my-app=gcr.io/google-samples/hello-app:2.0
kubectl rollout status -f deployment.yaml
kubectl scale --replicas=10 -f deployment.yaml && kubectl rollout status -f deployment.yaml
```

https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/