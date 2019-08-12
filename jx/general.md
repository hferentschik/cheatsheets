---
title: Dev Workflow
category: jx
layout: 2017/sheet
---

### List current environments 

Environment similar to workspace. 

```
> jx get environment
```

Contains "team" settings, which is the meta information about the workspace.

```
kubectl get env dev -o yaml
```

### Import quickstart

Import quickstart from default location [https://github.com/jenkins-x-quickstarts](https://github.com/jenkins-x-quickstarts):

```bash
> jx create quickstart
```

### Start a pipeline

```bash
> jx start pipleline
```

### Find logs for pull request

```bash
> jx get build log -f <pr-number>
```

### Garbage collect pods and activities

```bash
> jx gc pods
> jx gc activities
```

GC cleanup is also configured as _Cron Jobs_ in the cluster - jenkins-x-gcactivities, jenkins-x-gcpods, jenkins-x-gcpreviews.

### Interactive editing of jenkins-x.yaml

```bash
> jx create step
```

Also helpful to understand the pipeline kinds _release_, _pullrequest_, _feature_ as well as the lifecycle methods per pipline -   _setup_, _setversion_, _prebuild_, _build_, _postbuild_, _promote_.

### Show current ingress URLs

```bash
> jx open
```

or

```
> kubectl get ing
```

### Change the current Kuberentes namespace

Instead of using `kubectl`:

```bash
> jx ns
```
