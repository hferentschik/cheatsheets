---
title: Vault
category: jx
layout: 2017/sheet
intro: |
  All about Hashicorp's Vault usage in Jenkins X
---

### Use

Vault is the recommended way to store secrets for a Jenkins X installation.
When used with GKE or AWS, Vault is managed via Banzai Clouds [vault operator](https://github.com/banzaicloud/bank-vaults).
This means setup and key management is handled by the operator.
There is no "bring your own vault" option yet. 
For non GKE/AWS one needs to use the _local_ secret management.

### Access to Jenkins X system Vault

```bash
> eval $(jx get vault-config)
> vault kv list /secret # list secrets
> vault kv get /secret/auth/gitAuth.yaml # get a specific secret
> vault kv get -format json /secret/auth/gitAuth.yaml | jq -r .data.data.yaml | base64 -D
```

### Recover from a broken Vault install

Unable to unseal:

```bash
jx step boot vault
Installing vault-operator operator with helm values: [image.repository=banzaicloud/vault-operator image.tag=0.5.3]
Waiting for vault to be initialized and unsealed...
Waiting for vault to be initialized and unsealed...
```

To resolve delete and reinstall Vault:

```bash
# find system vault
> jx get vaults
NAME                  URL                               AUTH-SERVICE-ACCOUNT
jx-vault-hardy-jx-dev http://jx-vault-hardy-jx-dev:8200 jx-vault-hardy-jx-dev-auth-sa

# delete system vault
> jx delete vault jx-vault-hardy-jx-dev
Vault jx-vault-hardy-jx-dev deleted

# official route - re-run full boot
> jx boot

# reinstall just Vault
> cd <boot-config-dir>/systems/vault
> JX_INTERPRET_PIPELINE=true jx step boot vault
```
