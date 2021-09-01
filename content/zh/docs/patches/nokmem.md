---
title: nokmem
---

{{< link text="详细信息" url="https://bugzilla.redhat.com/show_bug.cgi?id=1507149" >}}

## Bug 影响

节点长期使用的时候提示剩余空间不足的错误，具体如下所示：

```
mkdir: cannot create directory '/sys/fs/cgroup/memory/8': No space left on device
```

节点磁盘充足但是一直报和这个错误, 并且创建 Pod 总是失败，这是一个潜在的“定时炸弹”。

## 影响范围

所有使用低版本内核的环境

k8s 1.22 之前的版本都受到影响, 在 runc 1.0.0-rc94 ({{< link text="opencontainers/runc#2840" url="https://github.com/opencontainers/runc/pull/2840" >}}) 修复(直接移除了)

## 防范措施

- 升级系统内核
- k8s 1.14 及以上
  - 重新构建 Kubelet 带上 `-tags=nokmem`
- k8s 1.14 以下
  - 硬编码, 可以参考 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.13.patch" >}}


### KLTS 修复的版本

- 1.18: 1.18.20-lts.1 {{< link text="nokmem.1.18.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.18.patch" >}}
- 1.17: 1.17.17-lts.1 {{< link text="nokmem.1.18.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.18.patch" >}}
- 1.16: 1.16.15-lts.1 {{< link text="nokmem.1.18.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.18.patch" >}}
- 1.15: 1.15.12-lts.1 {{< link text="nokmem.1.18.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.18.patch" >}}
- 1.14: 1.14.10-lts.1 {{< link text="nokmem.1.18.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.18.patch" >}}
- 1.13: 1.13.12-lts.1 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.13.patch" >}}
- 1.12: 1.12.10-lts.1 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.13.patch" >}}
- 1.11: 1.11.10-lts.1 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.13.patch" >}}
- 1.10: 1.10.13-lts.1 {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/master/patches/nokmem.1.13.patch" >}}