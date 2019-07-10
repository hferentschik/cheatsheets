---
title: Dev Workflow
category: jx
layout: 2017/sheet
intro: |
  Tips and tricks for writing tests for jx 
---

### Favour Ginko tests

* Ginko tests allow for creating test suites with proper setup and teardown hooks
* Easy to mark tests as pending via _X_ or _P_ prefix
* Use _F_ prefix for focused tests during development
* [Ginko](https://onsi.github.io/ginkgo/)
* [Gomega](http://onsi.github.io/gomega/)

### Use golden files when comparing against files in testdata

* Use [golden file](https://medium.com/soon-london/testing-with-golden-files-in-go-7fccc71c43d3) technique in order to easily update testdata when required.
