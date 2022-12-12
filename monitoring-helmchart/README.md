# Monitoring Helm Chart

Helm Chart include three dependency charts:
* Prometheus
* Grafana
* Blackbox Exporter

---

1. Create the namespace unitest and create main helm chart which has a dependencies:

```
kubectl create ?

helm create monitoring-helmchart
```

2. Install all needed repos:

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add grafana https://grafana.github.io/helm-charts

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

3. Create helm charts for prometheus, blackbox-exporter and grafana. Add in values.yaml files configuration. 
    - In grafana values.yaml add dashboard id and dataspource Prometheus.
    - In prometheus values.yaml add configuration for blackbox exporter.
    - In blackbox-exporter values.yaml add targets, which metrics need to monitor.
 


4. Add dependencies in main chart Chart.yaml.
```
dependencies:
  - name: prometheus
    version: 19.0.1
    repository: "file://charts/prometheus"
  - name: prometheus-blackbox-exporter
    version: 7.1.3
    repository: "file://charts/prometheus-blackbox-exporter"
  - name: grafana
    version: 6.47.1
    repository: "file://charts/grafana"

```

5. Update dependencies
```
helm dependency update --namespace unitest
```

6. Check if everything is correct
```
helm install monitoring-helmchart helm-unittest/monitoring-helmchart --dry-run --namespace unitest
```

7. Check pods
```
kubectl get pods --namespace unitest
```

----

Everything went smoothly until I had an issue with the 6 step and a bit stuck on this part. So for now I am working on the resolution of this error.