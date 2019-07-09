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
> kubectl get sourcerepository

# Tekton
> kubectl get pipelinerun
> kubectl get task
```

### Get Prow jobs using label selector

```bash
# comma seperate types if you want to filter on more than one
> kubectl get prowjob -l 'prow.k8s.io/type in (presubmit)'
```

* presubmit - pull request
* batch - batched pull request
* postsubmit - release
* peridoc - time based (Prow internal)

### Krew install

[krew](https://github.com/kubernetes-sigs/krew) is the package manager for kubectl plugins. Install [instructions](https://github.com/kubernetes-sigs/krew#installation).

### Krew list plugins

```bash
> kubectel krew list
```
