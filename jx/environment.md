---
title: Jenkins-X environments
category: jx
layout: 2017/sheet
intro: |
  Jenkins X environments
---

### Environment - what is it?

Environment is a core concept of Jenkins X.
An environment maps to a Kubernetes namespace.
Per default we have three environments - _dev_, _staging_ and _production_.
From a Jenkins X perspective _dev_ is most interesting, since it contains all the components needed to run Jenkins X.
Backed by the _Environment_ CRD.


### Get overview of running Jenkins X components

```bash
> jx get environment dev
```
