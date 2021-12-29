---
title: nokmem
weight: -100
short_description: |
  The node has sufficient disks, but it keeps reporting that the disk is insufficient to create a Pod.
---

{{< link text="Bug details" url="https://bugzilla.redhat.com/show_bug.cgi?id=1507149" >}}

The node has sufficient disks, but it keeps reporting that the disk is insufficient to create a Pod.

## Scope {#scope}

When the node is used for a long time, it prompts an error that the remaining space is insufficient. The error message is as follows:

```
mkdir: cannot create directory '/sys/fs/cgroup/memory/8': No space left on device
```

The node disk is sufficient but reports this error, and the creation of `Pod` always fails. This is a potential "time bomb".

All environments that use early-version kernels and Kubernetes versions before 1.22 will be affected. In runc 1.0.0-rc94 ({{< link text="opencontainers/runc#2840" url="https://github.com/opencontainers /runc/pull/2840" >}}) it has been fixed (removed directly).

## Prevention {#prevention}

- Upgrade the system kernel
- Kubernetes 1.14 or higher
  - Rebuild Kubelet with `-tags=nokmem`
- Kubernetes 1.14 or earlier
  - For hard coding, refer to {{< link text="nokmem.1.13.patch" url="https://github.com/klts-io/kubernetes-lts/raw/main/patches/nokmem.1.13.patch" >}}


## Fixed by KLTS {#klts-fixed}

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
