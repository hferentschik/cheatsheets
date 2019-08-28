---
title: Helm
category: tools
layout: 2017/sheet
---

### Jenkins-X Helm charts

The Helm charts for Jenkins-X can be found in the following repositories:

* [jenkins-x-platform](https://github.com/jenkins-x/jenkins-x-platform)
* [jenkins-x-charts](https://github.com/jenkins-x-charts)

### Helm install

```bash
> brew install helm
> kubectl create -f rbac-config.yaml
> helm init --service-account tiller --history-max 200
```

_rbac-config.yaml_
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```

See [Helm RBAC](https://helm.sh/docs/rbac/#role-based-access-control)
