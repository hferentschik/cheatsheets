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
: A Jenkins X extension.

Environment
: Place (namepsace) into which applications get deployed, e.g. the defaults _Dev_, _Staging_, _Production_.

Storage
: Persistent storage for build artifacts like logs, test or coverage reports.
  The artifact type is called a classifier.  
  The default storage is the git _gh-pages_ branch of the current application/environment.
  The recommended way, however, is to use a cloud bucket.
  To get the current storage configuration run: `jx get storage`. 
  To edit the storage settings: `jx edit storage` (see [#6226](https://github.com/jenkins-x/jx/issues/6226)).
