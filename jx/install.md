---
title: Jenkins-X installation
category: jx
layout: 2017/sheet
intro: |
  How to install Jenkins X 
---

### Installation

```bash
> jx create cluster gke --cluster-name hardy-jx-dev --zone us-central1-a --project-id $GC_PROJECT_ID --skip-login=true --skip-installation
> git clone git@github.com:jenkins-x/jenkins-x-boot-config.git
> cd jenkins-x-boot-config
> yq w -i jx-requirements.yml secretStorage vault    # using Vault
> yq w -i jx-requirements.yml cluster.gitPublic true # using public env repos 
> jx boot
```

### Uninstallation

```bash
> jx uninstall
```

### Installation flavors

* Prow vs Lighthouse
* TLS + LetsEncrypt vs nip.io
* Vault vs local secrets

### Common install problems

#### Unable to install Vault

```bash 
Waiting for vault to be initialized and unsealed...
error: creating system vault URL client: wait for vault to be initialized and unsealed: reading vault health: Error making API request.

URL: GET http://vault-jx.35.225.2.122.nip.io/v1/sys/health?drsecondarycode=299&performancestandbycode=299&sealedcode=299&standbycode=299&uninitcode=299
Code: 503. Raw Message:
```

Could be caused by an old Vault bucket which is in a different zone than the newly created cluster. 
Remedy by deleting the bucket and delete the faulty Vault install:

```bash
> jx get vaults
> jx delete valut -r <name>
```
