---
title: Concepts
category: jx
layout: 2017/sheet
intro: |
  Jenkins X Glossary Architecture
---

### Architecture

Event driven CI/CD system based on Kubernetes CRDs.

### Glossary

Application
: A deployed version of a project. 
Should be renamed to to for example `releases` to avoid confusion with Apps.

Apps
: A Jenkins X extension.

Environment
: Place where applications get deployed, e.g. Dev, Staging, Production.

Project
: A user's source code for a project, created by `jx import` or `jx create quickstart`.

