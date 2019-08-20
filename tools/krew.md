---
title: Krew
category: tools
layout: 2017/sheet
intro: |
   [krew](https://github.com/kubernetes-sigs/krew) - package manager for kubectl plugins. 
---

### Krew install

Install [instructions](https://github.com/kubernetes-sigs/krew#installation):

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
> kubectl krew list
```

### Access matrix plugin

Nice visualisation of RBAC permisssions for the current user.

#### Installation:

```bash
> kubectl krew install access-matrix
```

#### Usage:

```bash
> kubectl access-matrix
```
