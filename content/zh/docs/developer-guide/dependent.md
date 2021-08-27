---
title: "依赖"
weight: 30
---

## 安装 yq

{{< tabs >}}

{{% tab name="MacOS" %}}
``` bash
brew install jq python@3 # 安装 brew, 请看 https://brew.sh/
pip3 install yq
```
{{% /tab %}}

{{% tab name="基于 Red Hat 的发行版" %}}
``` bash
yum install -y epel-release
yum install -y jq python3
pip3 install yq
```
{{% /tab %}}

{{% tab name="基于 Debian 的发行版" %}}
``` bash
apt-get install -y jq python3 python3-pip
pip3 install yq
```
{{% /tab %}}

{{< /tabs >}}
