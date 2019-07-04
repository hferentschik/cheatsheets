---
title: Debugging
category: jx
layout: 2017/sheet
---

### Debugging jx within the cluster

To test controllers or pipeline steps in a running cluster against a dev version of `jx`, one can build the image locally, push it to a accessible image registry and then change the deployment config of the appropriate deployment to use this new image.

To build locally, using a short SHA to identify the image:

```bash
> make linux
> docker build -t hferentschik/jx:`git rev-parse --short HEAD` .
> docker push hferentschik/jx:`git rev-parse --short HEAD`
```

For smaller image sizes an Alpine image can be used:

```Dockerfile
FROM alpine:3.10

RUN apk --update add ca-certificates git

COPY ./build/linux/jx /usr/bin/jx
```

Once the image is pushed use `kubectl` or the Kube console to change the deployment config.
