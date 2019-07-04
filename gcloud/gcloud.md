---
title: Google cloud
category: gcloud
layout: 2017/sheet
intro: |
  Handy gcloud commands when running Jenkins-X cluster on GKE. 
---

### Open Cloud Console

To open a Google Cloud Console in a terminal

```sh
> gcloud alpha cloud-shell ssh
```

### Switching projects

```bash
> gcloud config set project [PROJECT_ID]
```

### Scale cluster

```bash
>  gcloud container clusters resize <cluster-name> --size <node-count>
```

### Building your own cloud shell image

Source for an example `Dockerfile` can be found in [jx-cloud-shell](https://github.com/hferentschik/jx-cloud-shell).

To build and use a custom image, you need to build in a cloudshell. In the cloud shell within a directory containing the `Dockerfile`:

```bash
> cloudshell env build-local

# To use image temporarily for current session
> cloudshell env push

# To push to GCloud repo
> cloudshell env push
```

Once the image is pushed, you can select it when you edit the Cloud Shell Environment.
