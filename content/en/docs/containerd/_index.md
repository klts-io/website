---
title: Containerd
weight: 200
---

## Kubernetes and Containerd Compatibility

The table below summarizes the latest Kubernetes-to-containerd recommendations
from the upstream containerd release policy.

| Kubernetes Version | Recommended containerd Version         | CRI Version |
| --- | --- | --- |
| 1.32 | 2.1.0+, 2.0.1+, 1.7.24+, 1.6.36+ | v1 |
| 1.33 | 2.1.0+, 2.0.4+, 1.7.24+, 1.6.36+ | v1 |
| 1.34 | 2.1.3+, 2.0.6+, 1.7.28+, 1.6.39+ | v1 |
| 1.35 | 2.2.0+, 2.1.5+, 1.7.28+ | v1 |

## References

- {{< link text="KLTS containerd-lts maintenance status" url="https://github.com/klts-io/containerd-lts/blob/main/README.md" >}}
- {{< link text="containerd upstream release and compatibility policy" url="https://github.com/containerd/containerd/blob/main/RELEASES.md" >}}
