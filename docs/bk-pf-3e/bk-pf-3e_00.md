## 前言

![介绍](img/httpatomoreillycomsourcenostarchimages2127149.png.jpg)

这是一本关于构建你所需网络的书。我们将从一些理论出发，探讨防火墙及相关功能的主题。你将看到许多关于过滤和其他网络流量引导方式的示例。我假设你已经具备基本到中级的 TCP/IP 网络概念和 Unix 管理知识。

本书中的所有信息都附带一个警告：正如许多工作一样，我们讨论的解决方案可以有多种实现方式。而且，软件世界总在变化，最好的做法可能已经发生了变化，本书的出版时间是在 2014 年 7 月，当时测试的是 OpenBSD 5.6 版、FreeBSD 10.0 版和 NetBSD 6.1 版以及当时可用的所有补丁。

## 这不是一本 HOWTO 手册

本书是我广受欢迎的 PF 教程的直接后代，也是该手稿的第三版。在这本书的编写过程中，我投入了大量精力，以确保它的实用性，我相信你会发现它很有用，并希望你也能享受阅读过程。但请记住，本书并不是一份可以直接复制粘贴的现成方案。

为了强调这一点，请跟我一起重复：

```
//The Pledge of the Network Admin//

This is my network.

It is mine,
or technically, my employer's.
It is my responsibility,
and I care for it with all my heart.

There are many other networks a lot like mine,

but none are just like it.

I solemnly swear

that I will not mindlessly paste from HOWTOs.
```

重点是，虽然我已经测试了本书中的所有配置，它们可能至少在某些方面不完全适用于你的网络。请记住，本书的目的是向你展示一些有用的技巧，并激励你做出更好的成果。

力求理解你的网络以及如何改进它，请不要盲目从本书或任何其他资料中复制粘贴。

## 本书内容

本书旨在成为一份独立的文档，使你能够在不需要频繁查阅手册页的情况下进行机器配置，并偶尔参考附录 A 中列出的在线和印刷资源。

你的系统可能会附带一个预写的*pf.conf*文件，其中包含了一些注释掉的有用配置建议，以及一些文档目录中的示例，比如*/usr/share/pf/*。这些示例作为参考是有用的，但我们在本书中不会直接使用它们。相反，你将学习如何从头开始一步步构建一个*pf.conf*文件。

这里是本书内容的简要概述：

+   第一章讲解了基本的网络概念，简要回顾了 PF 的历史，并为你提供了一些关于如何适应 BSD 操作系统的建议，如果你是这个操作系统家族的新手，建议先阅读这一章，以了解如何使用 BSD 系统。

+   第二章展示了如何在你的系统上启用 PF，并介绍了一个非常基础的单机规则集。该章相当重要，因为后续的所有配置都基于我们在这一章中构建的规则。

+   第三章 基于第二章中的单机配置，并引导你了解如何设置网关，作为不同网络之间的联络点。在第三章结束时，你将建立一个典型的家庭或小型办公室网络配置，并掌握一些技巧，便于简化网络管理。你还将提前体验如何处理具有特殊要求的服务，如 FTP，并获取一些关于如何通过支持一些常见但较少理解的互联网协议和服务来让网络更易于故障排除的小贴士。

+   第四章 引导你将无线网络添加到现有的设置中。无线环境带来了一些安全挑战，在本章结束时，你可能已经拥有了一个通过`authpf`实现访问控制和身份验证的无线网络。一些信息在有线环境中同样可能有所帮助。

+   第五章 讲解了当你引入需要从外部访问的服务器和服务时的情况。在本章结束时，你可能已经建立了一个拥有一个或多个独立子网和 DMZ（非军事区）的网络，并且你将尝试通过重定向和`relayd`来实现几种不同的负载均衡方案，以提高用户的服务质量。

+   第六章 介绍了 PF 工具箱中的一些工具，用于应对不良活动的尝试，并展示了如何有效地使用这些工具。我们处理了暴力破解密码尝试和其他网络洪水攻击，以及反垃圾邮件工具`spamd`，OpenBSD 的垃圾邮件推迟守护进程。本章应该让你的网络对合法用户更加友好，对那些心怀不良企图的人则不再那么热情。

+   第七章 介绍了通过 OpenBSD 5.5 引入的优先级和队列系统进行流量整形。本章还包含如何将早期基于 ALTQ 的设置转换为新系统的技巧，以及在没有新队列系统的操作系统上设置和维护 ALTQ 的信息。本章将帮助你通过根据网络需求调整流量整形来更好地利用资源。

+   第八章 介绍了如何创建冗余配置，使用 CARP 配置进行故障转移和负载均衡。本章将帮助你理解如何创建并维护一个高度可用、冗余的、基于 CARP 的配置。

+   第九章，解释了 PF 日志。你将学会如何使用系统自带工具以及可选包，从 PF 配置中提取并处理日志和统计数据。我们还将讨论基于 NetFlow 和 SNMP 的工具。

+   第十章，讲解了多种有助于调整配置的选项。它将你从前几章获得的知识与规则集调试教程结合起来。

+   附录 A，是一本注释过的印刷和在线文献及其他资源的列表，当你扩展 PF 和网络相关知识时，可能会对你有所帮助。

+   附录 B，概述了将一流工具作为自由软件开发时所涉及的一些问题。

本书的每一章都在前一章的基础上展开。虽然作为自由的个体，你完全可以跳过某些章节，但按顺序阅读章节可能会更有帮助。

由于种种原因，OpenBSD 是我最喜欢的操作系统。我写这本书的主要环境是由运行最近快照、偶尔是稳定版系统以及时不时构建的本地-current 版本的 OpenBSD 系统主导的。这意味着本书的主要视角是基于 OpenBSD 5.6 的命令行环境。然而，我保留了足够的其他 BSD 系统，因此即使你的平台选择是 FreeBSD、NetBSD 或 DragonFly BSD，这本书仍然会对你有用。在一些网络配置和 PF 设置的领域，这些系统与 OpenBSD 的基础系统有明显的差异，在这些情况下，你会找到关于差异的说明以及如何为你的环境构建有用配置的具体平台建议。
