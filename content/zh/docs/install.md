---
title: "安装步骤"
weight: 30
---

KLTS 提供了基于 deb 和 rpm 软件源的安装方式，您可以选择适合的安装方式。

安装前请确认已经完成了{{< link url="/docs/pre-install" >}}的安装。

## 设置 KLTS 软件源

{{< tabs >}}

{{% tab name="基于 Red Hat 的发行版" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://dl.klts.io/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="基于 Debian 的发行版" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://dl.klts.io/deb stable main
EOF

apt-get update
```
{{% /tab %}}


{{< tab name="基于 Red Hat 的发行版, 国内加速 🚀" >}}

<blockquote class="note callout">
  <div><strong>说明：</strong>以下加速均来自第三方, 安全和稳定性不做保障, 仅建议测试环境使用 ❗️❗️❗️ </div>
</blockquote>


    {{< tabs >}}

{{% tab name="/etc/hosts" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
curl https://raw.githubusercontent.com/wzshiming/github-hosts/master/hosts >>/etc/hosts

cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://dl.klts.io/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="hub.fastgit.org" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://hub.fastgit.org/klts-io/kubernetes-lts/raw/repos/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="ghproxy.com" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://ghproxy.com/https://raw.githubusercontent.com/klts-io/kubernetes-lts/repos/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="raw.githubusercontents.com" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.githubusercontents.com/klts-io/kubernetes-lts/repos/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

{{% tab name="raw.staticdn.net" %}}
执行以下代码设置下载 KLTS 的软件源：
``` bash
cat << \EOF > /etc/yum.repos.d/klts.repo
[klts]
name=klts
baseurl=https://raw.staticdn.net/klts-io/kubernetes-lts/repos/rpm/$basearch/
enabled=1
gpgcheck=0
EOF

yum makecache
```
{{% /tab %}}}

    {{< /tabs >}}

{{< /tab >}}

{{< tab name="基于 Debian 的发行版, 国内加速 🚀" >}}
执行以下代码设置下载 KLTS 的软件源：
<blockquote class="note callout">
  <div><strong>说明：</strong>以下加速均来自第三方, 安全和稳定性不做保障, 仅建议测试环境使用 ❗️❗️❗️ </div>
</blockquote>

    {{< tabs >}}

{{% tab name="/etc/hosts" %}}
``` bash
curl https://raw.githubusercontent.com/wzshiming/github-hosts/master/hosts >>/etc/hosts

cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://dl.klts.io/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="hub.fastgit.org" %}}
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://hub.fastgit.org/klts-io/kubernetes-lts/raw/repos/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="ghproxy.com" %}}
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://ghproxy.com/https://raw.githubusercontent.com/klts-io/kubernetes-lts/repos/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="raw.githubusercontents.com" %}}
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.githubusercontents.com/klts-io/kubernetes-lts/repos/deb stable main
EOF

apt-get update
```
{{% /tab %}}

{{% tab name="raw.staticdn.net" %}}
``` bash
cat << EOF > /etc/apt/sources.list.d/klts.list
deb [trusted=yes] https://raw.staticdn.net/klts-io/kubernetes-lts/repos/deb stable main
EOF

apt-get update
```
{{% /tab %}}

    {{< /tabs >}}

{{< /tab >}}

{{< /tabs >}}


## 安装

{{< tabs >}}
    {{< tab name="安装" >}}
        {{< tabs >}}

{{% tab name="基于 Red Hat 的发行版" %}}
``` bash
yum install kubeadm kubelet kubectl
```
{{% /tab %}}}

{{% tab name="基于 Debian 的发行版" %}}
``` bash
apt-get install kubeadm kubelet kubectl
```
{{% /tab %}}
        {{< /tabs >}}
    {{< /tab >}}

    {{< tab name="安装指定版本" >}}
        {{< tabs >}}

> 查看支持的版本
{{% tab name="基于 Red Hat 的发行版" %}}
``` bash
# 搜索支持的版本
yum search kubeadm --showduplicates | grep kubeadm-

# 安装
VERSION=1.18.20-lts.0
yum install kubeadm-v${VERSION} kubelet-v${VERSION} kubectl-v${VERSION}
```
{{% /tab %}}}

{{% tab name="基于 Debian 的发行版" %}}
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
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm config images pull --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

后续对 kubeadm 的操作都需要加上 --image-repository, --kubernetes-version 主动指定镜像

## 初始化控制面节点

``` bash
VERSION=1.18.20-lts.0
REPOS=ghcr.io/klts-io/kubernetes-lts
kubeadm init --image-repository ${REPOS} --kubernetes-version v${VERSION}
```

{{< link text="更多操作参考" url="https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/" >}}
