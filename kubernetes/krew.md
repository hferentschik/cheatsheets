---
title: Krew
category: kubernetes
layout: 2017/sheet
---

### Krew install

[krew](https://github.com/kubernetes-sigs/krew) is the package manager for kubectl plugins. Install [instructions](https://github.com/kubernetes-sigs/krew#installation).

```bash
> (
  set -x; cd "$(mktemp -d)" &&
  curl -fsSLO "https://storage.googleapis.com/krew/v0.2.1/krew.{tar.gz,yaml}" &&
  tar zxvf krew.tar.gz &&
  ./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" install \
    --manifest=krew.yaml --archive=krew.tar.gz
)
```

### Krew list plugins

```bash
> kubectel krew list
```
