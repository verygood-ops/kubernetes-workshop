## ClusterIP

  * This is the default for a service
  * It only exposes the service internally
  * You can access locally through port forward or proxy

```
kubectl apply -f cluster_ip.yaml
kubectl port-forward deployment/my-app 8080 8080
```

## NodePort

  * Exposes a port on a node `¯\_(ツ)_/¯`
  * The port is exposed on each node and routed to the appropriate service
  * Defaults to an ephemeral port in the 30000-32767 range

```
kubectl apply -f node_port.yaml
minikube service my-nodeport-service
```
