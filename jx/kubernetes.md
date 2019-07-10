---
title: Kubernets helpers
category: jx
layout: 2017/sheet
intro: |
  Some jx and kubectl commands useful when inspecting an Jenksins-X install. 
---

### Tailing logs of latest pipelinerunner deployment

```bash
> kubectl logs $(kubectl get pod -l app=pipelinerunner -o name) -f
```

### List all resources in the cluster

```bash
> kubectl api-resources --verbs=list -o name | xargs -n 1 kubectl get -o name
```

or to see the endpoints:

```bash
> kubectl api-resources -v=6
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

### Detect all resources for a given build

Assuming a repository name of _repo_ and the build number _11_:

```bash
> for i in pipelineactivity pipeline pipelinestructure taskrun pipelinerun task pod; do 
   kubectl get "$i" --show-kind --no-headers --ignore-not-found -l repository=demo,build=11
  done
```

Other labels which can be used: _branch_, _build_, _owner_, _repo_, _prowJobName_
