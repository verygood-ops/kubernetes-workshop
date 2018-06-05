# Quota Management

Creating limitation of your containers is one of the best practices.

When Kubernetes schedules a Pod, it’s important that the containers have enough resources to run. It's possible that you will schedule an application on a node with limited resources, and run out of memory or CPU and other things to stop working at all.

It’s also possible for applications to take up more resources than they should. This could be caused by a team spinning up more replicas, bad configuration change, resource leaking and so on, as a result some application can go out of control and take 100$ of available CPU. Regardless of whether the issue is caused by a bad developer, bad code, or bad luck, what’s important is that you'll be in control.

## Quota Types:
- Resource
- QoS

### Resource Limit Levels:
- node
- pod
- container

### QoS Classes
- Guaranteed (all resource limits and requests set)
- Burstable (one of resource limit or request set)
- Best-Effort (no limits/requests defined)

## Resource Quota

Launch tiny namespace and check it's limits:

```
kubectl create namespace tinyspace
kubectl -n tinyspace create -f ./05-Quota/resource-quotas.yaml
kubectl describe ns tinyspace
```

## CPU
launch container in new space and check node stats:
```
kubectl create -n tinyspace -f ./05-Quota/cpu-replication.yaml
```

scale it up:
```
kubectl -n tinyspace scale rc/cpuhog --replicas=2
```

and check:
```
kubectl -n tinyspace describe rc
[...]
  Warning  FailedCreate      2s (x15 over 8m)  replication-controller  (combined from similar events): Error creating: pods "cpuhog-ht2vk" is forbidden: exceeded quota: compute-resources, requested: limits.memory=1Gi,pods=1,requests.memory=1Gi, used: limits.memory=1Gi,pods=1,requests.memory=1Gi, limited: limits.memory=1Gi,pods=1,requests.memory=1Gi
```

delete cpuhog:
```
kubectl -n tinyspace delete -f ./05-Quota/cpu-replication.yaml
```

## OOM
Launch memory starving container:
```
kubectl create -f ./05-Quota/mem-starving.yaml
kubectl -n tinyspace describe pod
kubectl -n tinyspace describe pods <name>
```
Container will be killed by OOM error due to wrong limits

Cleanup:
```
kubectl delete deploy --all
```

## Memory QoS
Launch:
```
kubectl -n tinyspace create -f ./05-Quota/mem-guaranteed-replication.yaml
kubectl -n tinyspace create -f ./05-Quota/mem-burstable-replication.yaml
kubectl -n tinyspace create -f ./05-Quota/mem-besteffort-replication.yaml
```

## Cleanup:
```
kubectl delete deploy --all
```

## Minikube Cleanup:
```
minikube delete
```