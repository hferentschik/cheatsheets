---
title: Dev Workflow
category: jx
layout: 2017/sheet
---

### Change the current Kuberentes namespace

Instead of using `kubectl`:

```bash
> jx ns
```

### Start a pipeline

```bash
> jx start pipleline
```

### Find logs for pull request

```bash
> jx get build log -f <pr-number>
```
