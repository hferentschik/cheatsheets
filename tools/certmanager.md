---
title: CertManager
category: tools
layout: 2017/sheet
intro: |
  Everything around CertManager and Let's Encypt
---

### General

[cert-manager](https://github.com/jetstack/cert-manager) is a Kubernetes add-on to automate the management and issuance of TLS certificates from various issuing sources.

In Jenkins X cert-manager is used to get certificates from [Let's Encrypt](https://letsencrypt.org/).

cert-manager is installed in its own namespace _cert-manager_.
In this namespace there are two deployments created by the [Jenkins X Helm Chart](https://github.com/jenkins-x/jenkins-x-boot-config/tree/master/systems/cm) of cert-manager.

```bash
> kubectl get deployment -n cert-manager
```

### Get information about certificates

```bash
> kubectl get certificaterequest
> kubectl describe certificaterequest X
> kubectl get order
> kubectl describe order X
> kubectl get challenge
> kubectl describe challenge X
```
