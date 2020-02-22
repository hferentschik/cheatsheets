---
title: Debugging
category: jx
layout: 2017/sheet
intro: |
  Everything around debugging and troubleshooting jx issues
---

### Debuging Kube API

```
> TRACE_KUBE_API=1 jx <cmd>
```

### Debuging GitHub API

```
> TRACE_GITHUB_API=1 jx <cmd>
```

### Running jx dev versions within the cluster

To test controllers or pipeline steps in a running cluster against a dev version of `jx`, one can build the image locally, push it to a accessible image registry (eg Docker Hub) and then change the deployment config of the appropriate deployment to use this new image.

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

### Patching deployments 

Use [JSON Patch Builder Online](https://json-patch-builder-online.github.io/) to prepare your JSON patch, then execute `kubectl patch`. In the example below the pipelinerunner is patched where we want to replace the image at two different places:

```json
{
    "spec": {
        "containers": [
            {
                "args": [
                    "controller",
                    "pipelinerunner",
                    "--use-meta-pipeline",
                    "--meta-pipeline-image",
                    "hferentschik/jx:6f8018014",
                    "--verbose"
                ],
                "image": "hferentschik/jx:6f8018014",
            }
        ]
     }
 }                
```

```bash
> kubectl patch deployment pipelinerunner --type='json' -p='[
    {
        "op": "replace",
        "path": "/spec/template/spec/containers/0/image",
        "value": "hferentschik/jx:6f8018014"
    },
    {
        "op": "replace",
        "path": "/spec/template/spec/containers/0/args/4",
        "value": "hferentschik/jx:6f8018014"
    }
]'
```

### Patch pipelinerunner

```bash
function patch_pipelinerunner() {
 cd /Users/hardy/work/go/src/github.com/jenkins-x/jx
 gvm use system
 git stash apply $(git stash list | grep alpine | awk -F ':' '{print $1}')
 make linux
 tag=$(git rev-parse --short HEAD)
 docker build -t hferentschik/jx:$tag .
 docker push hferentschik/jx:$tag
 kubectl patch deployment pipelinerunner --type='json' -p='[
    {
        "op": "replace",
        "path": "/spec/template/spec/containers/0/image",
        "value": "hferentschik/jx:'$tag'"
    }
 ]'
}
```

### Debug issues with Prow jobs not occuring 

Start with checking the Prow config. If it looks ok, check the logs of the pipeline deployment.
The Prow pipeline controller is the entry point for the Prow jobs.

```bash
> kubectl log $(kubectl  get pods -l=app=pipeline --no-headers -o name)
```

### Using jq to process JSON logs locally

```bash
> JX_LOG_LEVEL=DEBUG JX_LOG_FORMAT=json jx controller pipelinerunner 2>&1 | jq 'map_values(if .|tostring|(test("\\[") or test("^{")) then (.|fromjson) else . end)'
```

Note: logs are currently written to stderr!

### List all images w/ version in cluster

```bash
> kubectl get pods -oyaml | grep 'image:' | awk -F ':' '{print $2 ":" $3}' | sort | uniq
```

### Run BDD tests against a fork/branch of bdd-jx

Clone https://github.com/jenkins-x/bdd-jx, branch, write test and push it to your remote.

Then in jx, edit the `ci.sh` script of the context in which you want to run the BDD test, eg `jx/bdd/boot-vault/ci.sh`:

```bash
jx step bdd \
    --versions-repo https://github.com/jenkins-x/jenkins-x-versions.git \
    --config ../jx/bdd/boot-vault/cluster.yaml \
    --gopath /tmp \
    --git-provider=github \
    --git-username $GH_USERNAME \
    --git-owner $GH_OWNER \
    --git-api-token $GH_ACCESS_TOKEN \
    --default-admin-password $JENKINS_PASSWORD \
    --no-delete-app \
    --no-delete-repo \
    --tests test-quickstart-golang-http \
    --tests test-app-lifecycle \
    --test-git-repo=<repo> \
    --test-git-branch=<branch>
```

Create a WIP pull request and watch the build logs.
