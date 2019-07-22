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

### Change the current Kuberentes namespace

Instead of using `kubectl`:

```bash
> jx ns
```
