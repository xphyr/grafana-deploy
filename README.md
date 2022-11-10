# grafana-deploy

```
oc apply -k kustomize/env/openshift-monitoring
oc apply -k kustomize/env/grafana-monitoring-operator
SATOKEN=`oc sa get-token grafana-thanos -n grafana-monitoring`
sed -i '' "s/Bearer .*/Bearer $SATOKEN/" kustomize/env/grafana-monitoring/kustomization.yaml
oc apply -k kustomize/env/grafana-monitoring
oc get route -n grafana-monitoring
```

Then use docs from here: https://docs.openshift.com/container-platform/4.10/monitoring/managing-metrics.html#specifying-how-a-service-is-monitored_managing-metrics


```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  labels:
    k8s-app: prometheus-example-monitor
  name: prometheus-example-monitor
  namespace: ns1
spec:
  endpoints:
  - interval: 30s
    port: web
    scheme: http
  selector:
    matchLabels:
      app: prometheus-example-app
```