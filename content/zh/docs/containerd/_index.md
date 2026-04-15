---
title: Containerd
weight: 200
---

## Kubernetes 与 Containerd 兼容性

下表整理了 containerd 社区最新发布策略中给出的 Kubernetes 与
containerd 推荐组合。

| Kubernetes 版本 | 推荐的 containerd 版本 | CRI 版本 |
| --- | --- | --- |
| 1.32 | 2.1.0+, 2.0.1+, 1.7.24+, 1.6.36+ | v1 |
| 1.33 | 2.1.0+, 2.0.4+, 1.7.24+, 1.6.36+ | v1 |
| 1.34 | 2.1.3+, 2.0.6+, 1.7.28+, 1.6.39+ | v1 |
| 1.35 | 2.2.0+, 2.1.5+, 1.7.28+ | v1 |

## 参考资料

- {{< link text="KLTS containerd-lts 维护状态" url="https://github.com/klts-io/containerd-lts/blob/main/README.md" >}}
- {{< link text="containerd 社区发布与兼容性策略" url="https://github.com/containerd/containerd/blob/main/RELEASES.md" >}}
