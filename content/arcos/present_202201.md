---
name: ARCOS present 01-2022
title: ARCOS presentation 01/2022
date: 2021-12-09-07:24:00+08:00
---

![mind map showing overview](/arcos/ARCOS_TWG_presentation_202201.svg)

```yaml
---
global:
  postgresql:
    postgresqlPassword: "xnat"
```

```bash
# Setup a terminal to view activity
watch kubectl -n xnat-demo get all,pvc

# Setup helm repo for AIS charts
helm repo add ais https://australian-imaging-service.github.io/charts
helm repo update

# Deploy
helm upgrade xnat ais/xnat --install --values ~/ARCOS/values.yaml --namespace xnat-demo --create-namespace

# Monitor logs
kubectl -nxnat-demo logs -f pod/xnat-xnat-web-0

kubectl -nxnat-demo port-forward service/xnat-xnat-web 8080:80
kubectl -nxnat-demo expose po xnat-xnat-web-0

helm test xnat --namespace xnat-demo
kubectl delete ns xnat-demo
```
