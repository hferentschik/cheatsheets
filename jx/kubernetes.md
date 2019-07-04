---
title: Kubernets helpers
category: jx
layout: 2017/sheet
---

### Change the current Kuberentes namespace

Instead of using `kubectl`:

```bash
> jx ns
```

### List all resources in the cluster

```bash
> kubectl api-resources --verbs=list -o name | xargs -n 1 kubectl get -o name
```

### CRDs

```bash
# Prow
> kubectl get prowjob

# Jenkins-X
> kubectl get pipelineactivity

# Tekton
> kubectl get pipelinerun
> kubectl get task
```

### Krew install

[krew](https://github.com/kubernetes-sigs/krew) is the package manager for kubectl plugins. Install [instructions](https://github.com/kubernetes-sigs/krew#installation).

### Krew list plugins

```bash
> kubectel krew list
```
