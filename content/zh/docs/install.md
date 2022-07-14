---
title: "正常安装"
weight: 30
---

KLTS 提供了基于 deb 和 rpm 软件源的安装方式，您可以选择适合的安装方式。

安装前请确认已经完成了{{< link url="/docs/pre-install" >}}工作。

## 设置 KLTS 软件源

{{< tabs >}}

{{% tab name="基于 Red Hat 的发行版" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontent.com/klts-io/kubernetes-lts/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://raw.githubusercontent.com/klts-io/others/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="基于 Debian 的发行版" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/kubernetes-lts/deb-v${VERSION} stable main
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/others/deb stable main
EOF

apt-get update
```
{{% /tab %}}


{{< tab name="基于 Red Hat 的发行版, 国内加速 🚀" >}}

<strong>说明：</strong>以下加速均来自第三方, 安全和稳定性不做保障, 仅建议测试环境使用 ❗️❗️❗️  <br><br>
执行以下代码设置下载 KLTS 的软件源：

    {{< tabs >}}

{{% tab name="/etc/hosts" %}}

``` bash
curl https://raw.githubusercontent.com/wzshiming/github-hosts/master/hosts >>/etc/hosts

VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontent.com/klts-io/kubernetes-lts/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://raw.githubusercontent.com/klts-io/others/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="hub.fastgit.org" %}}

``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://hub.fastgit.org/klts-io/kubernetes-lts/raw/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://hub.fastgit.org/klts-io/others/raw/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="ghproxy.com" %}}

``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://ghproxy.com/https://raw.githubusercontent.com/klts-io/kubernetes-lts/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://ghproxy.com/https://raw.githubusercontent.com/klts-io/others/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="raw.githubusercontents.com" %}}

``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontents.com/klts-io/kubernetes-lts/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://raw.githubusercontents.com/klts-io/others/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="raw.staticdn.net" %}}

``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.staticdn.net/klts-io/kubernetes-lts/rpm-v${VERSION}/\$basearch/
enabled=1
gpgcheck=0
[klts-other]
name=klts-others
baseurl=https://raw.staticdn.net/klts-io/others/rpm/\$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

    {{< /tabs >}}

{{< /tab >}}

{{< tab name="基于 Debian 的发行版, 国内加速 🚀" >}}
<strong>说明：</strong>以下加速均来自第三方, 安全和稳定性不做保障, 仅建议测试环境使用 ❗️❗️❗️<br><br>
执行以下代码设置下载 KLTS 的软件源：

    {{< tabs >}}

{{% tab name="/etc/hosts" %}}
``` bash
curl https://raw.githubusercontent.com/wzshiming/github-hosts/master/hosts >>/etc/hosts

VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/kubernetes-lts/deb-v${VERSION} stable main
deb [trusted=yes] https://raw.githubusercontent.com/klts-io/others/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="hub.fastgit.org" %}}
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://hub.fastgit.org/klts-io/kubernetes-lts/raw/deb-v${VERSION} stable main
deb [trusted=yes] https://hub.fastgit.org/klts-io/others/raw/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="ghproxy.com" %}}
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://ghproxy.com/https://raw.githubusercontent.com/klts-io/kubernetes-lts/deb-v${VERSION} stable main
deb [trusted=yes] https://ghproxy.com/https://raw.githubusercontent.com/klts-io/others/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="raw.githubusercontents.com" %}}
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontents.com/klts-io/kubernetes-lts/deb-v${VERSION} stable main
deb [trusted=yes] https://raw.githubusercontents.com/klts-io/others/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="raw.staticdn.net" %}}
``` bash
VERSION=1.18.20-lts.2
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.staticdn.net/klts-io/kubernetes-lts/deb-v${VERSION} stable main
deb [trusted=yes] https://raw.staticdn.net/klts-io/kubernetes-lts/deb stable main
EOF

apt-get update
```
{{% /tab %}}

    {{< /tabs >}}

{{< /tab >}}

{{< /tabs >}}


## 安装

{{< tabs >}}
{{% tab name="基于 Red Hat 的发行版" %}}
执行以下命令安装：
``` bash
yum install kubeadm kubelet kubectl
```
{{% /tab %}}}

{{% tab name="基于 Debian 的发行版" %}}
执行以下命令安装：
``` bash
apt-get install kubeadm kubelet kubectl
```
{{% /tab %}}
{{< /tabs >}}

## 开机自动启动 Kubelet
执行以下命令开机自动启动 Kubelet：
```
systemctl enable kubelet
```

## 拉取依赖镜像
{{< tabs >}}
{{% tab name="默认" %}}
执行以下命令 pull 依赖的镜像：
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
{{% /tab %}}}
{{% tab name="国内加速 🚀" %}}
执行以下命令 pull 依赖的镜像：
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.m.daocloud.io/klts-io/kubernetes-lts
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
{{% /tab %}}
{{< /tabs >}}

后续对 kubeadm 的操作都需要加上 `--image-repository` 和 `--kubernetes-version` 以主动指定镜像。

## 初始化控制面节点
{{< tabs >}}
{{% tab name="默认" %}}
执行以下命令初始化控制面的节点：
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
{{% /tab %}}}
{{% tab name="国内加速 🚀" %}}
执行以下命令初始化控制面的节点：
``` bash
VERSION=1.18.20-lts.2
REPOS=ghcr.m.daocloud.io/klts-io/kubernetes-lts
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```
{{% /tab %}}
{{< /tabs >}}

有关更多安装说明，请参阅 {{< link text="Kubernetes 操作指南" url="https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/" >}}。
