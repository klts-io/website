---
title: "Install with script"
weight: 30
---

KLTS provides a script that automates the installation process.

## Install


``` bash
wget https://github.com/klts-io/klts/raw/main/install.sh
chmod +x install.sh
./install.sh
```

``` console
Usage: ./install.sh [OPTIONS]
  -h, --help : Display this help and exit
  --kubernetes-container-registry=ghcr.io/klts-io/kubernetes-lts : Kubernetes container registry
  --kubernetes-version=1.18.20-lts.1 : Kubernetes version to install
  --containerd-version=1.3.10-lts.0 : Containerd version to install
  --runc-version=1.0.2-lts.0 : Runc version to install
  --kubernetes-rpm-source=https://github.com/klts-io/kubernetes-lts/raw/rpm-v1.18.20-lts.0 : Kubernetes RPM source
  --containerd-rpm-source=https://github.com/klts-io/containerd-lts/raw/rpm-v1.3.10-lts.0 : Containerd RPM source
  --runc-rpm-source=https://github.com/klts-io/runc-lts/raw/rpm-v1.0.2-lts.0 : Runc RPM source
  --others-rpm-source=https://github.com/klts-io/others/raw/rpm : Other RPM source
  --kubernetes-deb-source=https://github.com/klts-io/kubernetes-lts/raw/deb-v1.18.20-lts.0 : Kubernetes DEB source
  --containerd-deb-source=https://github.com/klts-io/containerd-lts/raw/deb-v1.3.10-lts.0 : Containerd DEB source
  --runc-deb-source=https://github.com/klts-io/runc-lts/raw/deb-v1.0.2-lts.0 : Runc DEB source
  --others-deb-source=https://github.com/klts-io/others/raw/deb : Other DEB source
  --focus=enable-iptables-discover-bridged-traffic,disable-swap,disable-selinux,setup-source,install-kubernetes,install-containerd,install-runc,install-crictl,install-cniplugins,setup-crictl-config,setup-containerd-cni-config,setup-kubelet-config,setup-containerd-config,daemon-reload,start-containerd,status-containerd,enable-containerd,start-kubelet,status-kubelet,enable-kubelet,images-pull,control-plane-init,status-nodes,show-join-command : Focus on specific step
  --skip='' : Skip on specific step
  ```

