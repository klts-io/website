---
title: "依赖"
weight: 30
---
本页介绍如何在不同的操作系统上安装依赖。
## 安装依赖

{{< tabs >}}

{{% tab name="MacOS" %}}
运行以下命令安装依赖：
``` bash
brew install jq git python@3 # 安装 brew, 请看 https://brew.sh/
pip3 install yq
```
{{% /tab %}}

{{% tab name="基于 Red Hat 的发行版" %}}
运行以下命令安装依赖：
``` bash
yum install -y epel-release
yum install -y jq git python3
pip3 install yq
```
{{% /tab %}}

{{% tab name="基于 Debian 的发行版" %}}
运行以下命令安装依赖：
``` bash
apt-get install -y jq git python3 python3-pip
pip3 install yq
```
{{% /tab %}}

{{< /tabs >}}
