# Monitoring with prometheus

**Prometheus** is a systems and service monitoring system. It collects metrics from configured targets at given intervals (pull model), evaluates rule expressions, displays the results, and can trigger alerts if some condition is observed to be true.

### In detail:
1. **Dimensional Data** Prometheus implements a highly dimensional data model. Time series are identified by a metric name and a set of key-value pairs.

1. **Queries**
Query language allows slicing and dicing of collected time series data in order to generate ad-hoc graphs, tables, and alerts.

1. **Visualization**
Prometheus has multiple modes for visualizing data: a built-in expression browser, Grafana integration, and a console template language.

1. **Storage**
Prometheus stores time series in memory and on local disk in an efficient custom format. Scaling is achieved by functional sharding and federation.

1. **Alerting**
Alerts are defined based on Prometheus's query language and maintain dimensional information. An alertmanager handles notifications and silencing.

1. **Integrations**
Existing exporters allow bridging of third-party data into Prometheus. Examples: system statistics, as well as Docker, HAProxy, StatsD, and JMX metrics.

1. **Client libraries** Client libraries allow easy instrumentation of services. Over ten languages are supported already and custom libraries are easy to implement.
