---
title: "Dependencies"
weight: 30
---
This page describes how you can install dependencies on different operating systems.
## Install dependencies

{{< tabs >}}

{{% tab name="MacOS" %}}
Run the following code to install the dependencies:
``` bash
brew install jq git python@3 # Install brew, See https://brew.sh/
pip3 install yq
```
{{% /tab %}}

{{% tab name="Red Hat-based distributions" %}}
Run the following code to install the dependencies:
``` bash
yum install -y epel-release
yum install -y jq git python3
pip3 install yq
```
{{% /tab %}}

{{% tab name="Debian-based distributions" %}}
Run the following code to install the dependencies:
``` bash
apt-get install -y jq git python3 python3-pip
pip3 install yq
```
{{% /tab %}}

{{< /tabs >}}
