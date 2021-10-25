---
title: "Clone"
weight: 20
---
This page describes how you can clone a Kubernetes master branch to your local computer.
## Clone single branch
Since the `repos` branch is used as a software source for RPM and DEB, it will be very large to directly clon it, so you shall try to only clone the master branch.
``` bash
git clone --single-branch -b master https://github.com/klts-io/kubernetes-lts
```
