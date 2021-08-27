---
title: "克隆"
weight: 30
---

## 克隆主分支

请尝试只克隆主分支, 由于 repos 仓库是作为 rpm 和 deb 的软件源的, 直接克隆全部的话会非常大

``` bash
git clone --single-branch -b master https://github.com/klts-io/kubepatch
```
