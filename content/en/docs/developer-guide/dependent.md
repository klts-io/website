---
title: "Dependent"
weight: 30
---

## Install dependencies

{{< tabs >}}

{{% tab name="MacOS" %}}
``` bash
brew install jq git python@3 # Install brew, See https://brew.sh/
pip3 install yq
```
{{% /tab %}}

{{% tab name="Red Hat-based distributions" %}}
``` bash
yum install -y epel-release
yum install -y jq git python3
pip3 install yq
```
{{% /tab %}}

{{% tab name="Debian-based distributions" %}}
``` bash
apt-get install -y jq git python3 python3-pip
pip3 install yq
```
{{% /tab %}}

{{< /tabs >}}
