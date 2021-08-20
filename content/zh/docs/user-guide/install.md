---
title: "安装"
weight: 30
---

KLTS 提供了基于 deb 和 rpm 的软件源的安装方式. 您可以选择适合自己系统的安装安装方式

安全前请确认已经完成了[相关依赖](/zh/documents/preinstall)的安装

## 设置 KLTS 软件源

{{< tabs >}}

{{% tab name="YUM" %}}
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontent.com/klts-io/kubepatch/repos/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="DEB" %}}
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/kubepatch/repos/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{< /tabs >}}


## 安装

{{< tabs >}}
    {{< tab name="安装" >}}
        {{< tabs >}}

{{% tab name="YUM" %}}
``` bash
yum install kubeadm kubelet kubectl
```
{{% /tab %}}}

{{% tab name="DEB" %}}
``` bash
apt-get install kubeadm kubelet kubectl
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}

    {{< tab name="安装指定版本" >}}
        {{< tabs >}}

> 查看支持的版本
{{% tab name="YUM" %}}
``` bash
# 搜索支持的版本
yum search kubeadm --showduplicates | grep kubeadm-

# 安装
VERSION=1.18.20-lts.0
yum install kubeadm-v${VERSION} kubelet-v${VERSION} kubectl-v${VERSION}
```
{{% /tab %}}}

{{% tab name="DEB" %}}
``` bash
# 搜索支持的版本
apt-cache show kubeadm | grep Version

# 安装
VERSION=1.18.20-lts.0
apt-get install kubeadm=${VERSION} kubelet=${VERSION} kubectl=${VERSION}
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}
{{< /tabs >}}

## 启动 Kubelet

```
systemctl enable --now kubelet
```

## 拉取依赖镜像

``` bash
VERSION=1.18.20-lts.0
REPOS=ghcr.io/klts-io/kubepatch
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

后续对 kubeadm 的操作都需要加上 --image-repository, --kubernetes-version 主动指定镜像

## 初始化控制面节点

``` bash
VERSION=1.18.20-lts.0
REPOS=ghcr.io/klts-io/kubepatch
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

[更多操作参考](https://kubernetes.io/zh/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
