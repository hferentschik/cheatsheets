---
title: Jenkins-X installation
category: jx
layout: 2017/sheet
intro: |
  How to install Jenkins X 
---

### Installation GKE

Create bucket for Terraform state:

```bash
> gsutil mb gs://my-tf-state-bucket/
```

Export _TF_VAR_gcp_project_:

```bash
> export TF_VAR_gcp_project=${GC_PROJECT_ID}
```

In empty directory in _main.tf_:

```terraform
terraform {
  backend "gcs" {
    bucket = "my-tf-state-bucket"
    prefix = "jx-dev"
  }
}

variable "gcp_project" {}

module "jx" {
  source = "jenkins-x/jx/google"

  gcp_project = var.gcp_project
  resource_labels = { created-by = "hardy", powered-by = "jenkins-x" }
}
```

```bash
> terraform init
> terraform apply
```

In another directory:

```bash
> jx boot -r <path-to-requirements-file>
```

### Uninstallation

```bash
> jx uninstall
```

To also delete the environment repositories:

```bash
> jx delete repo -o <repo-owner>
```

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
