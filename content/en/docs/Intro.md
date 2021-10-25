---
title: "Overview"
weight: 10
---
KLTS, known as Kubernetes Long Term Support, has a primary mission to provide free long-term maintenance support for earlier versions of Kubernetes.  

Kubernetes versions are expressed as **x.y.z**, where **x** is the major version, **y** is the minor version, and **z** is the patch version. For the versions maintained by KLTS, it is followed by a string beginning with **lts**.  

One of the reasons to maintain earlier versions is the fact that in a real production environment, the latest release is not the best or the most stable. In a normal case, As shown in the table below, a stable release of Kubernetes is not available until one year after the initial release of a particular version. For details see [Kubernetes release cycle](#kubernetes-release-cycle-release-cycle).

As shown below, 1.10 - 1.18 are the versions being maintained by KLTS, while 1.19 - 1.22 are the versions currently being maintained by the Kubernetes community, as described in the [Version Skew Policy](https://kubernetes.io/releases/version-skew-policy/#supported-versions)。

<img src="../klts_job.png" width="750">

Take 1.19 as an example, its stable release is expected to be available on October 28, 2021, but the stable release of 1.19 is not fully compatible with many features of 1.10 to 1.18, and there are countless iterations of development in between. If an enterprise rashly upgrades its kernel to 1.19, it is likely to cause production accidents. Other new versions such as 1.20 - 1.22 have similar problems.  

The choice of most enterprises today is to stay with earlier versions and not rush to upgrade. But the Kubernetes community only maintains the most recent four releases, how can you keep earlier versions safe from the CVE bugs and vulnerabilities that the community may discover from time to time? That's where KLTS comes in! We provide free maintenance support for earlier versions for up to three years.    

## KLTS release cycle {#maint-cycle}
KLTS currently maintains nine stable releases: 1.10.13, 1.11.10, 1.12.10. 1.13.12, 1.14.10, 1.15.12, 1.16.15, 1.17.17, 1.18.20.

If the Kubernetes community finds new CVE vulnerabilities or bugs, the KLTS team will take over those releases that the community has abandoned for maintenance and keep them in a continuous maintenance state. The current maintenance cycle for these nine releases is as follows.

![maintained by KLTS](../whatKLTSdoes.png)

As shown above, the Kubernetes community typically has a maintenance cycle of about one year for a minor version, while KLTS can provide long-term maintenance for the next three years until the code becomes obviously incompatible and the version will be phased out.
## Bug fix {#bug-fix}
As an example, the [CVE-2021-3121](https://www.cvedetails.com/cve/CVE-2021-3121) vulnerability discovered in January 2021 has a CVSS score of 7.5. However, as of September 2021 the Kubernetes community:  

- Only fixed four versions: 1.18, 1.19, 1.20, 1.21
- Announced that “all prior versions remain exposed and users should stop using them immediately”
- [Requests to fix earlier versions](https://github.com/kubernetes/kubernetes/issues/101435) are denied:

![CVE-2021-3121](../cve2021.png)

 KLTS addresses this situation by diligently fixing eight earlier versions that were heavily affected by the [CVE-2021-3121](https://www.cvedetails.com/cve/CVE-2021-3121) vulnerability. No complaints, no demands!

- v1.17.17
- v1.16.15
- v1.15.12
- v1.14.10
- v1.13.12
- v1.12.10
- v1.11.10
- v1.10.13  

 If you feel that the KLTS team's efforts are valuable and interesting to you, don’t hesitate to join the [KLTS community](https://github.com/klts-io) to talk and contribute.

## Kubernetes release cycle {#release-cycle}

| **Ver.** | **Initial release date** | **Stable release date** |
| :----------- | :--------------- | :------------------- |
| 1.10         | 2018-03-27       | 2019-02-13           |
| 1.11         | 2018-07-28       | 2019-05-01           |
| 1.12         | 2018-09-28       | 2019-07-08           |
| 1.13         | 2018-12-04       | 2019-10-15           |
| 1.14         | 2019-03-25       | 2019-12-11           |
| 1.15         | 2019-07-20       | 2020-05-06           |
| 1.16         | 2019-09-18       | 2020-09-02           |
| 1.17         | 2019-12-08       | 2021-01-13           |
| 1.18         | 2020-03-25       | 2021-06-18           |
| 1.19         | 2020-08-26       | 2021-10-28           |
| 1.20         | 2020-12-08       | 2022-02-28           |
| 1.21         | 2021-04-08       | 2022-06-28           |
| 1.22         | 2021-08-04       | 2022-10-28           |

An initial release refers to the first official release of a minor version such as 1.10.0, 1.11.0 ... 1.22.0, etc.  

A stable release is usually the final bug-fix release about one year after the initial release. It refers to the release of End Of Life (EOL), i.e., the community will not maintain this version from then on.  