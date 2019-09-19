---
title: Jenkins-X installation
category: jx
layout: 2017/sheet
intro: |
  Flavor of the day for installing jx 
---

### Installation

```bash
> jx create cluster gke --cluster-name hardy-jx-dev --zone us-central1-a --project-id $GC_PROJECT_ID --skip-login=true --skip-installation
> git clone git@github.com:jenkins-x/jenkins-x-boot-config.git
> cd jenkins-x-boot-config
> jx boot
```

Note, you can manually create cluster and skip `jx create` if you are not using gitops for the boot repo. 

### Uninstallation

```bash
> jx uninstall
```
