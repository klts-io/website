---
title: "Preparation"
weight: 20
---

<img src="https://raw.githubusercontent.com/kubernetes/kubeadm/master/logos/stacked/color/kubeadm-stacked-color.png" align="right" width="150px">This page introduces some pareparation before instalaltion. For example, it is required to firstly install the `kubeadm` toolbox. For information on how to create a cluster with kubeadm, see the {{< link url="/docs/install" >}} page.

## Before you begin

* A compatible Linux host. The Kubernetes project provides generic instructions for Linux distributions based on Debian and Red Hat, and those distributions without a package manager.
* 2 GB or more of RAM per machine (any less will leave little room for your apps).
* 2 CPUs or more.
* Good network connectivity between all nodes in the cluster (either public or on-premise network).
* The hostname, MAC address, and product_uuid shall be unique for every node. See {{< link text="here" url="#verify-mac-address" >}} for more details.
* Open the required ports on the host. See {{< link text="here" url="#check-required-ports" >}} for more details.
* Disable the swap partition. You **MUST** disable the swap partition to keep the kubelet working properly.

## Verify the MAC address and product_uuid are unique for every node {#verify-mac-address}

* Get the MAC address of the network interfaces using the command `ip link` or `ifconfig -a`
* Check the product_uuid using the command `sudo cat /sys/class/dmi/id/product_uuid`

It is very likely that hardware devices have unique addresses, although some virtual machines may use identical addresses. Kubernetes uses these values to uniquely identify the nodes in the cluster. If these values are not unique to each node, the installation process may {{< link text="fail" url="https://github.com/kubernetes/kubeadm/issues/31" >}}.

## Check network adapters

If you have more than one network adapter, and your Kubernetes components are not reachable via the default route, it is recommended to add IP route(s) so the Kubernetes cluster addresses go via the appropriate adapter.

## Letting iptables see bridged traffic

Make sure that the `br_netfilter` module is loaded. This can be done by running `lsmod | grep br_netfilter`. To load it explicitly, you can run the command `sudo modprobe br_netfilter`.

To enable the iptables on your Linux node to correctly see bridged traffic, you should ensure `net.bridge.bridge-nf-call-iptables` is set to 1 in your `sysctl` config, e.g.

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

For more details see the {{< link text="Network Plugin Requirements" url="https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/#network-plugin-requirements" >}} page.

## Check required ports
This section lists all ports that you may use on your nodes.
### Control-plane node(s)

| Protocol | Direction | Port Range | Purpose                 | Used By              |
| -------- | --------- | ---------- | ----------------------- | -------------------- |
| TCP      | Inbound   | 6443\*     | Kubernetes API server   | All                  |
| TCP      | Inbound   | 2379-2380  | etcd server client API  | kube-apiserver, etcd |
| TCP      | Inbound   | 10250      | kubelet API             | Self, Control plane  |
| TCP      | Inbound   | 10251      | kube-scheduler          | Self                 |
| TCP      | Inbound   | 10252      | kube-controller-manager | Self                 |

### Worker node(s)

| Protocol | Direction | Port Range  | Purpose            | Used By             |
| -------- | --------- | ----------- | ------------------ | ------------------- |
| TCP      | Inbound   | 10250       | kubelet API        | Self, Control plane |
| TCP      | Inbound   | 30000-32767 | NodePort Services† | All                 |

Above is the default port range for {{< link text="NodePort Services" url="https://kubernetes.io/docs/concepts/services-networking/service/" >}}.

Any port numbers marked with * are overridable, so you will need to ensure any custom ports you provide are also open.

Although etcd ports are included in control-plane nodes, you can also host your own etcd cluster externally or on custom ports.

The pod network plugin you use (see below) may also require certain ports to be open. Since this differs with each pod network plugin, see the
documentation for the plugins about what port(s) those need.

## Setting a host name

Set a hostname for your host by using the following command:

``` bash
hostnamectl set-hostname your-new-host-name
echo "127.0.0.1 $(hostname)" >> /etc/hosts
echo "::1       $(hostname)" >> /etc/hosts
```

## Disable Swap

Run the following command to disable the partition swap:

``` bash
swapoff -a
```

If you want to disable swap permanently, edit the `/etc/fstab` file to comment out the swap mount.

## Disable Selinux

Run the following command to disable the selinux:

``` bash
setenforce 0
```

If you want to disable selinux permanently, edit `/etc/sysconfig/selinux` and replace `SELINUX=enforcing` with `SELINUX=disabled`.

## Install Runtime{#installing-runtime}

To run containers in Pods, Kubernetes uses a Container Runtime Interface (CRI).

{{< tabs name="container-runtimes" >}}
{{% tab name="Linux Node" %}}

By default, Kubernetes uses a CRI to interface with your chosen container runtime.

If you don't specify a runtime, kubeadm automatically tries to detect an installed container runtime by scanning through a list of well known Unix domain sockets. The following table lists container runtimes and their associated socket paths:

| Runtime    | Path to Unix domain socket      |
| ---------- | ------------------------------- |
| Docker     | /var/run/dockershim.sock        |
| Containerd | /run/containerd/containerd.sock |
| CRI-O      | /var/run/crio/crio.sock         |


<br/>
If both Docker and Containerd are detected, Docker takes precedence. This is inevitable because Docker 18.09 ships with Containerd and both are detectable even if you only installed Docker. If any other two or more runtimes are detected, kubeadm exits with an error.

The kubelet integrates with Docker through the built-in `dockershim` CRI implementation.


{{% /tab %}}
{{% tab name="Other OS" %}}
By default, kubeadm uses Docker as the container runtime. The kubelet integrates with Docker through the built-in `dockershim` CRI implementation.

{{% /tab %}}
{{< /tabs >}}


{{< tabs >}}
    {{< tab name="Docker" >}}
        {{< tabs >}}

{{% tab name="Red Hat-based distributions" %}}
Run the following command to install a Red Hat-based distribution:

``` bash
yum install docker
```
{{% /tab %}}


{{% tab name="Debian-based distributions" %}}
Run the following command to install a Debian-based distribution:

``` bash
apt-get install docker.io
```
{{% /tab %}}

        {{< /tabs >}}
    {{< /tab >}}

{{% tab name="Containerd" %}}

By default, Containerd only provides download packages for the amd64 architecture. If you are using a different architecture, you can install the `containerd.io` package from the official Docker repository. Instructions for setting up the Docker repository and installing the `containerd.io` package for your respective Linux distribution can be found in {{< link text="Installing the Docker Engine" url="https://docs.docker.com/engine/install/#server" >}}.

You can also use the following source code to build.

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

See {{< link text="container runtimes" url="https://kubernetes.io/docs/setup/production-environment/container-runtimes/" >}} for more information.
