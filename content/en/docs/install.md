---
title: Step-By-Step Install
weight: 30
---

KLTS provides a way to install source packages based on Deb and RPM. You can choose the installation method that suits your system.

Before installation, ensure that your {{< link url="/docs/pre-install" >}} is good enough.
## Set the KLTS source package

{{< tabs >}}

{{% tab name="Red Hat-based distributions" %}}
Run the following code to set the source of downloading a proper distribution:
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontent.com/klts-io/kubernetes-lts/rpm-${VERSION}/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="Debian-based distributions" %}}
Run the following code to set the source of downloading a proper distribution:
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/kubernetes-lts/deb-${VERSION} stable main
EOF

apt-get update
```
{{% /tab %}}

{{< /tabs >}}

## Install

{{< tabs >}}
    {{< tab name="Install" >}}
        {{< tabs >}}

{{% tab name="Red Hat-based distributions" %}}
Run the following code to install a proper distribution:
``` bash
yum install kubeadm kubelet kubectl
```
{{% /tab %}}}

{{% tab name="Debian-based distributions" %}}
Run the following code to install a proper distribution:
``` bash
apt-get install kubeadm kubelet kubectl
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}

    {{< tab name="Install the specified releases" >}}
        {{< tabs >}}

> View the supported releases
{{% tab name="Red Hat-based distributions" %}}
Run the following code to install a proper distribution:
``` bash
# Search for supported releases
yum search kubeadm --showduplicates | grep kubeadm-

# Install
VERSION=1.18.20-lts.2
yum install kubeadm-v${VERSION} kubelet-v${VERSION} kubectl-v${VERSION}
```
{{% /tab %}}}

{{% tab name="Debian-based distributions" %}}
Run the following code to install a proper distribution:
``` bash
# Search for supported releases
apt-cache show kubeadm | grep Version

# Install
VERSION=1.18.20-lts.2
apt-get install kubeadm=${VERSION} kubelet=${VERSION} kubectl=${VERSION}
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}
{{< /tabs >}}

## Auto-start Kubelet on boot
Run the following code to start Kubelet on boot:
```
systemctl enable kubelet
```
## Pull the dependency image
Run the following code to pull the dependency image:
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
All subsequent operations on Kubeadm need to include `--image-repository` and `--kubernetes-version` to actively specify the image.
## Initialize the control plane node
Run the following code to initialize the control plane node:
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
For details see {{< link text="Create a cluster with kubeadm" url="https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/" >}}.
