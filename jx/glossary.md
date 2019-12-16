---
title: Glossary
category: jx
layout: 2017/sheet
intro: |
  Jenkins X Glossary
---

### Glossary

Application
: A user's source code for a project, created by `jx import` or `jx create quickstart`.
  Use `jx [get|delete] application` to manage.

Apps
: A Jenkins X extension (might change its name to extension/plugin).

Boot Configuration
: A repository containing the current configuration of the Jenkins X cluster and installation.
  Usually one starts of with a clone [jenkins-x-boot-config](https://github.com/jenkins-x/jenkins-x-boot-config) of and then manages the configuration via GitOps simialar to the Environment repositories.
  See also the [boot](https://jenkins-x.io/docs/getting-started/setup/boot/) online docs.
 
Environment
: Place (namepsace) into which applications get deployed, e.g. _Staging_ or _Production_.

Storage
: Persistent storage for build artifacts like logs, test or coverage reports.
  The artifact type is called a classifier.  
  The default storage is the git _gh-pages_ branch of the current application/environment.
  The recommended way, however, is to use a cloud bucket.
  To get the current storage configuration run: `jx get storage`. 
  To edit the storage settings: `jx edit storage` (see [#6226](https://github.com/jenkins-x/jx/issues/6226)).
