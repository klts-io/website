---
title: "安装预备"
weight: 20
---

## 设置节点名字

``` bash
hostnamectl set-hostname your-new-host-name
echo "127.0.0.1 $(hostname)" >> /etc/hosts
echo "::1       $(hostname)" >> /etc/hosts
```

## 关闭 Swap

``` bash
swapoff -a
```

如需要永久关闭请编辑 `/etc/fstab` 文件注释掉 swap 的挂载

## 关闭 Selinux

``` bash
setenforce 0
```

如需要永久关闭请编辑 `/etc/sysconfig/selinux` 把 `SELINUX=enforcing` 替换为 `SELINUX=disabled`

## 安装容器运行时

{{< tabs name="cri" >}}
{{{< tab name="Containerd" codelang="bash" >}}
VERSION=1.5.4
wget -c https://github.com/containerd/containerd/releases/download/v${VERSION}/containerd-${VERSION}-linux-amd64.tar.gz
tar xvf containerd-${VERSION}-linux-amd64.tar.gz -C /usr/local/
mkdir /etc/containerd/ && containerd config default > /etc/containerd/config.toml
wget -c -O /etc/systemd/system/containerd.service https://raw.githubusercontent.com/containerd/containerd/main/containerd.service
systemctl start containerd && systemctl enable containerd
{{< /tab >}}
{{< tab name="YUM-Docker" codelang="bash" >}}
yum install docker
{{< /tab >}}}
{{{< tab name="DEB-Docker" codelang="bash" >}}
apt-get install docker.io
{{< /tab >}}
{{< /tabs >}}


## 最后在安装前还需确认

- 我的任意节点 hostname 都不是 localhost，且不包含下划线、小数点、大写字母, 这将作为 Kubernetes 的 Node 名
- 我的任意节点都有固定的内网 IP 地址
- 我的任意节点上 IP 地址（无需 NAT 映射即可相互访问），且没有防火墙、安全组隔离

