---
title: "Overview"
weight: 10
---
KLTS, known as Kubernetes Long Term Support, has a primary mission to provide free long-term maintenance support for early versions of Kubernetes.  

One of the reasons to maintain early versions is the fact that in a real production environment, the latest release is not the best or the most stable. In a normal case, a of Kubernetes is not available until one year after the initial release of a particular version. For details see [Kubernetes release cycle](#release-cycle). After the community aborts maintenance, KLTS will continue to maintain it in the next three years.  

Why is the choice of most enterprises today to stay with early versions and not rush to upgrade?  

- Firstly, the high frequency of upgrades may cause more risks and each upgrade must be fully verified. In the financial industry, the change cycle of a PaaS platform is usually relatively long, because once the updated version has a bug, it needs to be forced to roll back or quickly respond and upgrade to a updated version, which will cause unnecessary expenditures.  

- Secondly, once an enterprise upgrades their the Kubernetes kernel, some functional alternatives may not yet fully ready for production, and incompatibility often occurs in the production environment.  

- Finally, the Kubernetes community only supports minor version upgrades one by one, and does not support cross-version upgrades, because the later upgrades often have some uncontrollable factors that may cause some production problems.  

Therefore, the choice of most enterprises today is to stay with early versions and not rush to upgrade. But the Kubernetes community only maintains the most recent three to four releases, how can you keep early versions safe from the CVE bugs and vulnerabilities that the community may discover from time to time? That’s where KLTS comes in! We provide free maintenance support for early versions for up to three years, actively fix the CVE vulnerabilities and critical bugs.  
## KLTS release cycle {#maint-cycle}
Kubernetes versions are expressed as x.y.z, where x is the major version, y is the minor version, and z is the patch version. For the versions maintained by KLTS, it is followed by a string beginning with lts. For the convenience of communication, people often use the first two digits x.y to describe the Kubernetes version.  


Assuming that the latest Kubernetes released by the community is x.y, according to the [Version Skew Policy](https://kubernetes.io/releases/version-skew-policy/#supported-versions), the community only maintains the latest three versions, and KLTS currently maintains nearly ten early versions starting from 1.10, as shown in the figure below.  

<img src="../klts_job.png" width="750">  

When the Kubernetes community discovers new CVE vulnerabilities or bugs that may affect production, it may be affected not only the versions that the community is maintaining, but also the early versions that have been discontinued before but are still in use by some enterprises and cannot be upgraded rashly, which are maintained by the KLTS team. The current maintenance cycle of KLTS is as follows:  

![versions maintained by KLTS](../whatKLTSdoes.png)

As shown above, the maintenance cycle of a certain version by the Kubernetes community is usually about one year, and KLTS can provide a long-term maintenance in the next three years until the code is incompatible, and then the corresponding version will be aborted.  
## Bugs fixed by KLTS {#bug-fix}
Some high-priority CVEs or serious bugs in the production environment may cause greater security risks. CVE security issues are the lifeblood of the cluster, so KLTS will fix mid-to-high-risk CVEs, and then fix major bugs to guarantee stable operation of the production environment.  

As an example, the [CVE-2021-3121](https://www.cvedetails.com/cve/CVE-2021-3121) vulnerability discovered in January 2021 has a CVSS score of 7.5. However, as of September 2021 the Kubernetes community:  

- Only fixed four versions: 1.18, 1.19, 1.20, 1.21
- Announced that “all prior versions remain exposed and users should stop using them immediately”
- Requests to [fix early versions](https://github.com/kubernetes/kubernetes/issues/101435) are denied:

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

If you feel that the KLTS team’s efforts are valuable and interesting to you, don’t hesitate to join the [KLTS community](https://github.com/klts-io) to talk and contribute.
## Welcome to talk and join {#klts-benefits}
After careful maintenance and diligent support by developers, KLTS brings the following results to these early versions:

- **Three-year maintenance period**: KLTS will provide continuous maintenance for up to three years once the Kubernetes community aborts maintenance.
- **Safe and stable**: Minor version upgrades are safer with high compatibility. This kind of progressive upgrade is more stable. For example, the new features provided by the latest version may be very attractive, but it may not be able to meet the standards available for production and require a long time to adapt.
- **Easy to install**: Combined with domestic image acceleration, it natively supports Kubeadm, and CentOS, Ubuntu, and openSUSE, and also provides a one-click installation script.
- **Open and transparent**: KLTS is an open source project hosted on GitHub and the whole process is open.
- **more in roadmap**: Long-term maintenance of Containerd and other components will be added later.

Here is a sincere invitation to developers. If you feel that the KLTS team’s contributions are valuable and make you trustworthy, you are welcome to join the KLTS community to talk and contribute. We look forward to any comments, suggestions, or solutions.

- [KLTS community](https://github.com/klts-io)
- [KLTS Slack channel](https://klts.slack.com/archives/C02H8DMB6SZ)

## Kubernetes release cycle {#release-cycle}
The release cycle of recent ten versions by the Kubernetes community are as follows:

| **Ver.** | **Initial date** | **EOL date** |
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

An initial date refers to the date of first official release of a minor version such as 1.10.0, 1.11.0 … 1.22.0, etc.  

An EOL date refers to the date of End Of Life (EOL) release, i.e., the community will not maintain this version from then on. This is the final bug-fix release about one year after the initial release.
