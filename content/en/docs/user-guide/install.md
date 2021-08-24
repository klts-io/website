---
title: Install
weight: 30
---

KLTS provides a way to install software sources based on Deb and RPM. 
You can choose the installation method that suits your system

Before installation, ensure that [related dependencies](/zh/documents/preinstall) has been installed

## Set the KLTS software source

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


## Install

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

    {{< tab name="Install the specified releases" >}}
        {{< tabs >}}

> View the supported releases
{{% tab name="YUM" %}}
``` bash
# Search for supported releases
yum search kubeadm --showduplicates | grep kubeadm-

# Install
VERSION=1.18.20-lts.0
yum install kubeadm-v${VERSION} kubelet-v${VERSION} kubectl-v${VERSION}
```
{{% /tab %}}}

{{% tab name="DEB" %}}
``` bash
# Search for supported releases
apt-cache show kubeadm | grep Version

# Install
VERSION=1.18.20-lts.0
apt-get install kubeadm=${VERSION} kubelet=${VERSION} kubectl=${VERSION}
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}
{{< /tabs >}}

## Start Kubelet

```
systemctl enable --now kubelet
```

## Pull the dependency image

``` bash
VERSION=1.18.20-lts.0
REPOS=ghcr.io/klts-io/kubepatch
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

All subsequent operations on Kubeadm need to include --image-repository, --kubernetes-version actively specifying the image

## Initialize the control plane node

``` bash
VERSION=1.18.20-lts.0
REPOS=ghcr.io/klts-io/kubepatch
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

[More Reference](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
