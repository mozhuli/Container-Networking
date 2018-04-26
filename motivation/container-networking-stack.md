# 1.3 容器网络技术栈

&emsp;&emsp;容器网络技术栈包含以下内容：

## 低层网络层

&emsp;&emsp;包括网络设备，iptables，路由，IPVLAN和Linux命名空间。除非你从事容器网络相关的工作，否则通常不需要知道该层的细节，但至少应该知道这一点。请注意，这里的技术已经存在并被使用了十年以上。

## 容器网络层

&emsp;&emsp;该层提供了一些抽象，如单主机桥接网络模式和多主机IP-per-container解决方案。我将在第2章和第3章中介绍了这一层。

## 容器编排层

&emsp;&emsp;在这里，容器调度程序在调度容器的时候需要由较低层提供部分网络信息。在第4章中，我们将简要介绍下容器编排系统，在第5章中我们将重点讨论服务发现方面的内容。第6章讨论容器网络标准CNI，最后在第7章讨论Kubernetes网络。

***软件定义网络***

&emsp;&emsp;*SDN实际上是一个营销术语。采用SDN，网络管理团队变得更加敏捷，并且可以对不断变化的业务需求做出更快的反应。 SDN是使用软件对网络进行配置，无论是通过API补充[网络功能虚拟化](https://en.wikipedia.org/wiki/Network_function_virtualization)还是通过软件构建网络。特别是如果您是开发人员或架构师，我建议您快速浏览思科对此主题的[精彩概述](https://www.cisco.com/web/solutions/trends/sdn/index.html)以及SDxCentral的文章“[什么是软件定义的网络（SDN）](https://bit.ly/2jvUkiO)？”*

&emsp;&emsp;如果你在网络运维团队，那么你可能很乐意马上阅读下一章。 但是，如果您是架构师或开发人员，并且您的网络知识可能有点生疏，我建议在大概学习完[Linux网络管理员指南](http://www.tldp.org/LDP/nag2/nag2.pdf)之后进行下一步学习。
