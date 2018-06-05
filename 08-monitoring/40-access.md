### Accessing the monitoring bundle

```bash
# Check cluster access:
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.2", GitCommit:"81753b10df112992bf51bbc2c2f85208aad78335", GitTreeState:"clean", BuildDate:"2018-05-12T04:12:12Z", GoVersion:"go1.9.6", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"9", GitVersion:"v1.9.4", GitCommit:"bee2d1505c4fe820744d26d41ecd3fdd4a3d6546", GitTreeState:"clean", BuildDate:"2018-03-12T16:21:35Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
$ kubectl get nodes
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     master    29m       v1.9.4
$ kubectl get pods --all-namespaces
...
```

All monitoring services have type ClusterIP by default. There's a [hack](https://stevesloka.com/2017/05/19/access-minikube-services-from-host/) 
to access them easily from host, but we will create another set of services of type NodeIP. 

More on service types [here](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)
```bash 
$ kubectl get svc
NAME                                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
alertmanager-operated                 ClusterIP   None             <none>        9093/TCP,6783/TCP   34m
kube-grafana                          NodePort    10.99.181.231    <none>        3000:31919/TCP      24m
kube-prometheus                       ClusterIP   10.109.228.167   <none>        9090/TCP            34m
kube-prometheus-alertmanager          ClusterIP   10.108.95.30     <none>        9093/TCP            34m
kube-prometheus-exporter-kube-state   ClusterIP   10.96.106.5      <none>        80/TCP              34m
kube-prometheus-exporter-node         ClusterIP   10.102.169.13    <none>        9100/TCP            34m
kube-prometheus-grafana               ClusterIP   10.101.253.90    <none>        80/TCP              34m
prometheus-operated                   ClusterIP   None             <none>        9090/TCP            34m

kubectl expose service kube-grafana --type=NodePort --name my-grafana
kubectl expose service kube-prometheus --type=NodePort --name my-prometheus
kubectl expose service kube-prometheus-alertmanager --type=NodePort --name my-alerts

# Get new service ports
kubectl get service | grep my-

# Get minikube ip
minikube status

# Open each service like:
open http://MINIKUBE_IP:SERVICE_PORT
```