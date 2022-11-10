# grafana-deploy

```
oc apply -k kustomize/env/openshift-monitoring
oc apply -k kustomize/env/grafana-monitoring-operator
SATOKEN=`oc sa get-token grafana-thanos -n grafana-monitoring`
sed -i '' "s/Bearer .*/Bearer $SATOKEN/" kustomize/env/grafana-monitoring/kustomization.yaml
oc apply -k kustomize/env/grafana-monitoring
oc get route -n grafana-monitoring
```