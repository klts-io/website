---
title: "Dependent"
weight: 30
---

## Install yq

{{< tabs >}}

{{% tab name="MacOS" %}}
``` bash
brew install jq python@3 # Install brew, See https://brew.sh/
pip3 install yq
```
{{% /tab %}}

{{% tab name="Red Hat-based distributions" %}}
``` bash
yum install -y epel-release
yum install -y jq python3
pip3 install yq
```
{{% /tab %}}

{{% tab name="Debian-based distributions" %}}
``` bash
apt-get install -y jq python3 python3-pip
pip3 install yq
```
{{% /tab %}}

{{< /tabs >}}
