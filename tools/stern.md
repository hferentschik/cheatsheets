---
title: stern
category: tools
layout: 2017/sheet
intro: |
  [stern](https://github.com/wercker/stern) - Multi pod and container log tailing for Kubernetes
---

### Install

```bash
> brew install stern
```

### Usage

```bash
> stern -s 5m -n jx .
```

Last argument is the pod query and can be adjusted to just target a specific pod.
