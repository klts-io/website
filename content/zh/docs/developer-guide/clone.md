---
title: "克隆"
weight: 20
---
本页介绍如何将 Kubernetes master 分支克隆到本地。
## 克隆主分支
请尝试只克隆主分支，由于 repos 仓库作为 rpm 和 deb 的软件源，直接克隆全部会非常大。

可执行以下命令克隆主分支：

``` bash
git clone --single-branch -b main https://github.com/klts-io/kubernetes-lts
```
