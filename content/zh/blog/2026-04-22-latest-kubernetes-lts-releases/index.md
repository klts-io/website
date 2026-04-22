---
layout: blog
title: "KLTS 最新 Kubernetes LTS 版本更新（2026 年 4 月 22 日）"
date: 2026-04-22
---

我们已将最新的 Kubernetes LTS 版本信息同步到 KLTS 网站。本次更新对应 2026 年 4 月 22 日发布的一批 KLTS release。

## 最新版本

| Kubernetes 小版本 | 最新 KLTS 版本 |
| --- | --- |
| v1.32 | [v1.32.13-lts.2](/docs/kubernetes/releases/v1.32/v1.32.13-lts.2/) |
| v1.31 | [v1.31.14-lts.2](/docs/kubernetes/releases/v1.31/v1.31.14-lts.2/) |
| v1.30 | [v1.30.14-lts.2](/docs/kubernetes/releases/v1.30/v1.30.14-lts.2/) |
| v1.29 | [v1.29.15-lts.2](/docs/kubernetes/releases/v1.29/v1.29.15-lts.2/) |
| v1.28 | [v1.28.15-lts.3](/docs/kubernetes/releases/v1.28/v1.28.15-lts.3/) |
| v1.27 | [v1.27.16-lts.2](/docs/kubernetes/releases/v1.27/v1.27.16-lts.2/) |
| v1.26 | [v1.26.15-lts.2](/docs/kubernetes/releases/v1.26/v1.26.15-lts.2/) |
| v1.25 | [v1.25.16-lts.2](/docs/kubernetes/releases/v1.25/v1.25.16-lts.2/) |
| v1.24 | [v1.24.17-lts.2](/docs/kubernetes/releases/v1.24/v1.24.17-lts.2/) |
| v1.23 | [v1.23.17-lts.2](/docs/kubernetes/releases/v1.23/v1.23.17-lts.2/) |
| v1.22 | [v1.22.17-lts.2](/docs/kubernetes/releases/v1.22/v1.22.17-lts.2/) |
| v1.21 | [v1.21.14-lts.3](/docs/kubernetes/releases/v1.21/v1.21.14-lts.3/) |
| v1.20 | [v1.20.16-lts.1](/docs/kubernetes/releases/v1.20/v1.20.16-lts.1/) |
| v1.19 | [v1.19.16-lts.4](/docs/kubernetes/releases/v1.19/v1.19.16-lts.4/) |
| v1.18 | [v1.18.20-lts.3](/docs/kubernetes/releases/v1.18/v1.18.20-lts.3/) |
| v1.17 | [v1.17.17-lts.3](/docs/kubernetes/releases/v1.17/v1.17.17-lts.3/) |
| v1.16 | [v1.16.15-lts.3](/docs/kubernetes/releases/v1.16/v1.16.15-lts.3/) |

## 4 月 22 日发布重点

- v1.21 到 v1.32 分支已更新为 Go 1.25.9 构建。
- 较新的发布线按分支继承当前 KLTS 镜像、registry、代码生成和 etcd 维护补丁链。
- 当前安全回补继续在 Kubernetes 补丁文档中维护，并已在更新后的 release 页面中体现。

## Kubernetes 社区更新（WG-LTS）

Kubernetes 社区已于 **2026 年 3 月 26 日** 合并 [kubernetes/community#8889](https://github.com/kubernetes/community/pull/8889)，并正式将 WG-LTS 进入 spindown（停止运作）状态。

- WG-LTS 已从社区工作组列表及 `sigs.yaml` 中移除。
- 2025 年度报告中记录了 spindown 状态，并引用了公开公告/提案链接：[WG-LTS 停止运作公告](https://groups.google.com/a/kubernetes.io/g/wg-lts/c/e4XyeS19BsU)。

## 相关安全更新

同时已同步以下 CVE 文档：

- [CVE-2024-10220](/docs/kubernetes/patches/cve-2024-10220/)
- [CVE-2024-9042](/docs/kubernetes/patches/cve-2024-9042/)
- [CVE-2025-0426](/docs/kubernetes/patches/cve-2025-0426/)
- [CVE-2025-13281](/docs/kubernetes/patches/cve-2025-13281/)
- [CVE-2025-1767](/docs/kubernetes/patches/cve-2025-1767/)
- [CVE-2025-5187](/docs/kubernetes/patches/cve-2025-5187/)

完整更新请查看：
- [/docs/kubernetes/releases/](/docs/kubernetes/releases/)
- [/docs/kubernetes/patches/](/docs/kubernetes/patches/)
