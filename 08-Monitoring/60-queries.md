### Prometheus queries

```
# CPU Usage per container
sum (rate (container_cpu_usage_seconds_total{image!=""}[1m])) by (container_name)

# Memory Usage per container (limited by kube-system namespace)
sum by(container_name) (container_memory_usage_bytes{namespace="kube-system"})

# Node CPU usage (per core)
100 * (1 - (irate(node_cpu{mode="idle"}[5m])))

```

- [Query functions](https://prometheus.io/docs/prometheus/latest/querying/functions/)
- [Official Examples](https://prometheus.io/docs/prometheus/latest/querying/examples/)
- [More Examples](https://github.com/infinityworks/prometheus-example-queries)
