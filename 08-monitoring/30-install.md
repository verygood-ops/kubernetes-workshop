### Installing with helm
```bash
# Launch minikube
minikube start --memory 4096 --kubernetes-version v1.9.4 --bootstrapper kubeadm

# Install helm
brew install helm

# Init helm agent on a cluster
helm init

# Add coreos repo
helm repo add coreos https://s3-eu-west-1.amazonaws.com/coreos-charts/stable/

# Install prometheus operator
helm install coreos/prometheus-operator --name prometheus-operator --namespace monitoring

# Install prometheus monitoring bundle
helm install coreos/kube-prometheus --name kube-prometheus --namespace monitoring
```
### What's in a bundle:
- [Docs](https://github.com/coreos/prometheus-operator/tree/master/contrib/kube-prometheus#kube-prometheus)