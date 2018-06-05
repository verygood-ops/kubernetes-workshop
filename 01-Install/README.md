# Install a local Kubernetes cluster

[Minikube](https://github.com/kubernetes/minikube) is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.

## Installation
### macOS
```shell
brew update && brew install kubectl && brew cask install docker minikube virtualbox
```
> You may need to allow the Oracle installation under `Security & Privacy`

### Linux
```shell
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

### Windows
Download the [minikube-windows-amd64.exe](https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe) file, rename it to `minikube.exe` and add it to your path.

## Running the cluster

`minikube start`

## Auto Completion

### Mac
```
## If running Bash 3.2 included with macOS
brew install bash-completion
## or, if running Bash 4.1+
brew install bash-completion@2
echo "source <(kubectl completion bash)" >> ~/.bash_profile
```

### Linux
```
echo "source <(kubectl completion bash)" >> ~/.bashrc
```

## Helm

https://github.com/kubernetes/helm/blob/master/docs/install.md#installing-the-helm-client

### Mac
```
brew install kubernetes-helm
```

### Windows

```
choco install kubernetes-helm
```

### Script

```
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
```

### Tiller

```
helm init
```

## Commands

```
kubectl get ns
kubectl get po --all-namespaces
kubectl get po [pod_name] -o yaml
kubectl -n kube-system get po -l integration-test=storage-provisioner
```
