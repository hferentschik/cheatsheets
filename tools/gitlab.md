---
title: Gitlab
category: tools
layout: 2017/sheet
intro: |
  How to get GitLab running  
---

### Install

Make sure Helm is installed.

```bash
> jx ns gitlab --create
> helm repo add gitlab https://charts.gitlab.io/
> helm repo update
> helm install gitlab/gitlab -n gitlab  --timeout 600 -f ./values.yaml
```

_values.yaml_
```yaml
# Minimal settings
global:
  ingress:
    configureCertmanager: false
    class: "nginx"
  hosts:
    domain: <ip>.nip.io
    externalIP: <ip>
# Don't use certmanager, we'll self-sign
certmanager:
  install: false
# Use the `ingress` addon, not our Ingress (can't map 22/80/443)
nginx-ingress:
  enabled: false
# GitLab Runner isn't a big fan of self-signed certificates
gitlab-runner:
  install: false
```

```bash
> kubectl get secret gitlab-gitlab-initial-root-password -ojsonpath='{.data.password}' | base64 --decode ; echo
```

* https://docs.gitlab.com/charts/installation/deployment.html
* https://docs.gitlab.com/charts/development/minikube/


