---
title: "Introduction"
weight: 10
---
## Versions {#klts-ver}
This section describes the meaning of a version provided by KLTS.


<img src="../klts_ver.png" width="300">

As shown in the figure above, V1.16.15 is the complete version number of a kubernetes release, where 1.16 is the major version and 15 is a patch from the community. The final part, such as lts.0, is the patch version provided by KLTS.

## What does KLTS maintain for Kubernetes? {#klts-job}
This section describes the kubernetes versions that KLTS can support. 


<img src="../klts_job.png" width="750">

The figure above shows the latest version of kubernetes as of August 31, 2021 was 1.22. In a normal case, the Kubernetes community only maintains four recent versions, such as 1.19 to 1.22. 


How and where can you get the earlier versions that the Kubernetes community does not maintain but your company is still using the verions in a production or equivalent environment? This is one of the reason why KLTS is set up here. 


As of August 31, 2021, KLTS maintains those earlier versions from 1.10 to 1.18. We promise to maintain each earlier version at least two years. Kubernetes 1.10 is the production kernel built in DaoCloud Enterprise 3.0, a PaaS platform developed by daocloud.io, and may be maintained for a relatively longer period. 


The Kubernetes community generally releases a major version every 4 months or so, and the Kubernetes versions maintained by KLTS will change accordingly. Typically, within a month after the Kubernetes community stops to maintain a version, KLTS will take over to maintain it in a month.


If some bugs or critical vulnerables are fixed by the KLTS team, we will upload the fixed version here for the community members to download and use it freely.


For example, if the community officially releases version 1.23, the highest version maintained by KLTS will be increased by a patch number to 1.19, and so on. In general, KLTS patches will be released as often as the bugs are actually resolved.