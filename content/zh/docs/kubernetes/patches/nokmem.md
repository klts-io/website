---
title: nokmem
weight: -100
short_description: |
  节点磁盘充足但是一直报磁盘不足无法创建 `Pod`。
---

{{< link text="Bug 详情" url="https://bugzilla.redhat.com/show_bug.cgi?id=1507149" >}}

节点磁盘充足但是一直报磁盘不足无法创建 `Pod`。

## Bug 影响 {#scope}

节点长期使用的时候提示剩余空间不足的错误，报错信息如下所示：

```
mkdir: cannot create directory '/sys/fs/cgroup/memory/8': No space left on device
```

节点磁盘充足但是一直报和这个错误, 并且创建 `Pod` 总是失败，这是一个潜在的“定时炸弹”。

所有使用低版本内核的环境以及 Kubernetes 1.22 之前的版本都会受到影响，在 runc 1.0.0-rc94 ({{< link text="opencontainers/runc#2840" url="https://github.com/opencontainers/runc/pull/2840" >}}) 进行了修复(被直接移除)。

## 防范措施 {#prevention}

- 升级系统内核
- Kubernetes 1.14 及以上
  - 重新构建 Kubelet 带上 `-tags=nokmem`
- Kubernetes 1.14 以下
  - 有关硬编码，请参考 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}


## KLTS 修复的版本 {#klts-fixed}

- {{< link url="/docs/kubernetes/releases/v1.19.16/v1.19.16-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.18.20/v1.18.20-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.17.17/v1.17.17-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.16.15/v1.16.15-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.15.12/v1.15.12-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.14.10/v1.14.10-lts.1/" >}} {{< link text="nokmem.1.19.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.19.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.13.12/v1.13.12-lts.1/" >}} {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.12.10/v1.12.10-lts.1/" >}} {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.11.10/v1.11.10-lts.1/" >}} {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}
- {{< link url="/docs/kubernetes/releases/v1.10.13/v1.10.13-lts.1/" >}} {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}
