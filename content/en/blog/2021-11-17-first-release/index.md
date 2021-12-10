---
layout: blog
title: "Official release of KLTS"
date: 2021-11-17
---

We are happy to announce that the KLTS project is officially launched. KLTS is suitable for enterprise users and can be directly used in a production environment. After the Kubernetes community stops maintaining a certain version, KLTS will continue to provide maintenance for two to three years, mainly including patching CVE vulnerabilities and fixing serious bugs.

KLTS team took more than 2 months from proposing ideas, organizing code, building acceleration channels and websites, and finally launching it online. Our purpose is to share and communicate, sharing makes people happy, and communication makes progress.

Why do we need the KLTS project? The reason is that the official Kubernetes community only maintains the latest 3 - 4 versions, but those earlier versions are still used in many actual production environments. If you rashly upgrade to a new version, it is easy to cause production failures.

We have encountered such a case.
## Upgrade issues
In July 2021, a bank customer directly upgraded Kubernetes 1.11 to 1.18. When the customer performed a stress test in the upgraded business system, a serious failure occurred in the production environment.

The bank’s management and our company’s leaders both showed great considerations to this matter, and immediately organized experts to work overtime and try to reproduce the failure situation again. The two large inter-provincial production clusters were investigated node by node. After repeated attempts, they finally found the right direction and succeeded. They successfully located the critical point at which the failure occurs.

After several tests, it was finally determined that the migration of the Master node from old to new cluster nodes caused a large-scale failure of the new cluster network. Some features supported by the old Master were not well supported after the upgrade.

Afterwards, a bank executive reported: “The reason for upgrading the old system is because of a security vulnerability in Kubernetes 1.11, but we never expected such a large-scale failure after the upgrade.”

## Internal discussion
The occurrence of such failures often affects the actual production and triggers a series of serious consequences. So after this incident, we conducted detailed internal discussions and realized that earlier versions of Kubernetes running in the production environment cannot be rushed to upgrade to the new version, which can easily cause various unforeseen problems and customers may also be in a dilemma.

In order to improve customer satisfaction, we have continued to maintain those earlier versions of Kubernetes from 1.10 over the past two years to solve different failures. Often a colleague received an after-sales service call late at night, immediately started remote investigation after quickly cleaning his face with cold water, and outside was almost bright when he solved the problem and looked out of the window again.

After fighting day and night for more than two years, we fixed many bugs and solved countless failures. After this bank incident, our team realized that these maintained versions of Kubernetes are digital assets that many enterprises cannot ask for.

”The team put forward a big suggestion: "Can these versions be shared with the open source community and benefit more users? Not just limited to our company's customers, it can also contribute some to the community development."

Just as the Kubernetes Community Day (KCD) conference was held globally, this proposal received positive responses from our team members.

## Build
Do whatever it takes. The first step is to pick up the patches that have been fixed over the years from our code repository. Then rely on Github's CI, resume testing, build software sources (YUM/DEB), images, and websites, and write documents.

All these releases have been fully tested in CentOS7.

## Official release
In November 2021, it is the golden autumn season. Once everything is ready, [KLTS](https://klts.io/zh/) is officially released. We hope that the experience accumulated by our colleagues over the past few years can bring you some help and you can avoid detours.

Since 1.10, all kernels have been verified by financial, government, and enterprise production environment. You can download it with confidence and directly put it into the production environment after being simple tested and verified.

If you have any comments or questions, feel free to reach out to us in the following ways:
  * [Slack](https://klts.slack.com/archives/C02H8DMB6SZ)
  * [KLTS community](https://github.com/klts-io)
