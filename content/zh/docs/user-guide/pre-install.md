---
title: "安装预备"
weight: 20
---

<img src="https://raw.githubusercontent.com/kubernetes/kubeadm/master/logos/stacked/color/kubeadm-stacked-color.png" align="right" width="150px">本页面显示如何安装 `kubeadm` 工具箱。
有关在执行此安装过程后如何使用 kubeadm 创建集群的信息，请参见
[使用 kubeadm 创建集群](/zh/docs/user-guide/install/) 页面。

## 准备开始

* 一台兼容的 Linux 主机。Kubernetes 项目为基于 Debian 和 Red Hat 的 Linux
  发行版以及一些不提供包管理器的发行版提供通用的指令
* 每台机器 2 GB 或更多的 RAM （如果少于这个数字将会影响你应用的运行内存)
* 2 CPU 核或更多
* 集群中的所有机器的网络彼此均能相互连接(公网和内网都可以)
* 节点之中不可以有重复的主机名、MAC 地址或 product_uuid。请参见[这里](#verify-mac-address)了解更多详细信息。
* 开启机器上的某些端口。请参见[这里](#check-required-ports) 了解更多详细信息。
* 禁用交换分区。为了保证 kubelet 正常工作，你 **必须** 禁用交换分区。

## 确保每个节点上 MAC 地址和 product_uuid 的唯一性    {#verify-mac-address}

* 你可以使用命令 `ip link` 或 `ifconfig -a` 来获取网络接口的 MAC 地址
* 可以使用 `sudo cat /sys/class/dmi/id/product_uuid` 命令对 product_uuid 校验

一般来讲，硬件设备会拥有唯一的地址，但是有些虚拟机的地址可能会重复。
Kubernetes 使用这些值来唯一确定集群中的节点。
如果这些值在每个节点上不唯一，可能会导致安装
[失败](https://github.com/kubernetes/kubeadm/issues/31)。

<!--
## Check network adapters

If you have more than one network adapter, and your Kubernetes components are not reachable on the default
route, we recommend you add IP route(s) so Kubernetes cluster addresses go via the appropriate adapter.
-->
## 检查网络适配器

如果你有一个以上的网络适配器，同时你的 Kubernetes 组件通过默认路由不可达，我们建议你预先添加 IP 路由规则，这样 Kubernetes 集群就可以通过对应的适配器完成连接。

## 允许 iptables 检查桥接流量

确保 `br_netfilter` 模块被加载。这一操作可以通过运行 `lsmod | grep br_netfilter`
来完成。若要显式加载该模块，可执行 `sudo modprobe br_netfilter`。

为了让你的 Linux 节点上的 iptables 能够正确地查看桥接流量，你需要确保在你的
`sysctl` 配置中将 `net.bridge.bridge-nf-call-iptables` 设置为 1。例如：

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sudo sysctl --system
```

更多的相关细节可查看[网络插件需求](https://kubernetes.io/zh/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/#network-plugin-requirements)页面。

## 检查所需端口{#check-required-ports}

### 控制平面节点

| 协议 | 方向 | 端口范围  | 作用                    | 使用者                       |
| ---- | ---- | --------- | ----------------------- | ---------------------------- |
| TCP  | 入站 | 6443      | Kubernetes API 服务器   | 所有组件                     |
| TCP  | 入站 | 2379-2380 | etcd 服务器客户端 API   | kube-apiserver, etcd         |
| TCP  | 入站 | 10250     | Kubelet API             | kubelet 自身、控制平面组件   |
| TCP  | 入站 | 10251     | kube-scheduler          | kube-scheduler 自身          |
| TCP  | 入站 | 10252     | kube-controller-manager | kube-controller-manager 自身 |

### 工作节点

| 协议 | 方向 | 端口范围    | 作用           | 使用者                     |
| ---- | ---- | ----------- | -------------- | -------------------------- |
| TCP  | 入站 | 10250       | Kubelet API    | kubelet 自身、控制平面组件 |
| TCP  | 入站 | 30000-32767 | NodePort 服务† | 所有组件                   |

[NodePort 服务](https://kubernetes.io/zh/docs/concepts/services-networking/service/) 的默认端口范围。

使用 * 标记的任意端口号都可以被覆盖，所以你需要保证所定制的端口是开放的。

虽然控制平面节点已经包含了 etcd 的端口，你也可以使用自定义的外部 etcd 集群，或是指定自定义端口。

你使用的 Pod 网络插件 (见下) 也可能需要某些特定端口开启。由于各个 Pod 网络插件都有所不同，
请参阅他们各自文档中对端口的要求。

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

## 安装 runtime{#installing-runtime}

为了在 Pod 中运行容器，Kubernetes 使用 
容器运行时（Container Runtime）


{{< tabs name="container-runtimes" >}}
{{% tab name="Linux 节点" %}}

默认情况下，Kubernetes 使用 容器运行时接口（Container Runtime Interface，CRI）
来与你所选择的容器运行时交互。

如果你不指定运行时，则 kubeadm 会自动尝试检测到系统上已经安装的运行时，
方法是扫描一组众所周知的 Unix 域套接字。
下面的表格列举了一些容器运行时及其对应的套接字路径：

| 运行时     | 域套接字                        |
| ---------- | ------------------------------- |
| Docker     | /var/run/dockershim.sock        |
| Containerd | /run/containerd/containerd.sock |
| CRI-O      | /var/run/crio/crio.sock         |


<br/>
如果同时检测到 Docker 和 containerd，则优先选择 Docker。
这是必然的，因为 Docker 18.09 附带了 containerd 并且两者都是可以检测到的，
即使你仅安装了 Docker。
如果检测到其他两个或多个运行时，kubeadm 输出错误信息并退出。

kubelet 通过内置的 `dockershim` CRI 实现与 Docker 集成。


{{% /tab %}}
{{% tab name="其它操作系统" %}}
默认情况下， kubeadm 使用 docker 作为容器运行时。
kubelet 通过内置的 `dockershim` CRI 实现与 Docker 集成。

{{% /tab %}}
{{< /tabs >}}


{{< tabs >}}
    {{< tab name="Docker" >}}
        {{< tabs >}}

{{% tab name="YUM" %}}
``` bash
yum install docker
```
{{% /tab %}}


{{% tab name="DEB" %}}
``` bash
apt-get install docker.io
```
{{% /tab %}}

        {{< /tabs >}}
    {{< /tab >}}

{{% tab name="Containerd" %}}
``` bash
VERSION=1.5.4
wget -c https://github.com/containerd/containerd/releases/download/v${VERSION}/containerd-${VERSION}-linux-amd64.tar.gz
tar xvf containerd-${VERSION}-linux-amd64.tar.gz -C /usr/local/
mkdir /etc/containerd/ && containerd config default > /etc/containerd/config.toml
wget -c -O /etc/systemd/system/containerd.service https://raw.githubusercontent.com/containerd/containerd/main/containerd.service
systemctl start containerd && systemctl enable containerd
```
{{% /tab %}}

{{< /tabs >}}

参阅[容器运行时](https://kubernetes.io/zh/docs/setup/production-environment/container-runtimes/)
以了解更多信息。