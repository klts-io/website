---
title: "简介"
weight: 10
---
本页为您介绍 KLTS 的 Kubernetes 版本支持机制。   
<img src="../klts_ver.png" width="300">

如图所示，V1.16.15 是 Kubernetes 的完整发行版本号，其中 1.16 是大版本号，15 是社区补丁版本，而 lts.0 是 KLTS 的补丁版本号。 

<img src="../klts_job.png" width="750">

上图以 2021 年 8 月 31 日的最新版本 1.22 为例，Kubernetes 社区仅维护 1.19 – 1.22 四个版本。而 KLTS 则提供从 1.10 到 1.18 的版本维护，每个版本的支持周期至少两年。其中 Kubernetes 1.10 是 DaoCloud Enterprise 3.0 的生产内核，其维护周期会相对更长。我们会将修复 bug 后的稳定版本上传至 KLTS，供社区下载使用。

Kubernetes 社区一般每隔 4 个月左右发布一个大版本，KLTS 维护的 Kubernetes 版本也会随之变化。通常在 Kubernetes 社区停止维护某个版本后的一个月内，KLTS 将开始维护刚被社区停止维护的版本。  

例如，如果社区正式发布 1.23 版本，KLTS 维护的版本也会加一，达到 1.19，以此类推。KLTS 的补丁更新频率将根据实际解决的 bug 情况发布。

