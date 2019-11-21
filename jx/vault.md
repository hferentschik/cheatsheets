---
title: Vault
category: jx
layout: 2017/sheet
---

### Recover from a broken Vault install

Problems like:

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
