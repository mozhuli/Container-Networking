# 1.4 我需要全盘押注容器吗？

&emsp;&emsp;当我参加各种会议或用户组时，我常遇到因容器技术所带来的机遇而倍感兴奋的人。 与此同时，他们比较迷茫，需要对容器技术押注多大的砝码才能从中受益。 下表展示了我对目前业界使用容器技术情况的非正式概述，按照不同的阶段进行了分组：

| 阶段 | 典型的配置 | 例子 |
| :---: | :----: | :----: |
| 传统 | 物理机或虚拟机，无容器 | 目前大多数产品的部署方式 |
|  简单使用  | 用于应用程序依赖管理而手动启动容器     | 开发和测试环境 |
|  定制化  | 用于管理容器而自定义的本地调度程序   | RelateIQ, Uber |
|  全面爆发  | 使用第4章中的调度程序来管理容器，容错，自我修复   | Google, Zulily, Gutefrage.de |

&emsp;&emsp;请注意，全面爆发阶段不一定与部署的规模相符。 例如，Gutefrage.de只有6个裸机服务器在管理，但使用Apache Mesos来管理它们，并且您可以[在Raspberry Pi上轻松运行Kubernetes集群](https://www.hanselman.com/blog/HowToBuildAKubernetesClusterWithARMRaspberryPiThenRunNETCoreOnOpenFaas.aspx)。

&emsp;&emsp;到目前为止，您可能已经意识到我们正在处理分布式系统。 鉴于我们通常希望将容器部署到计算机网络中，我强烈建议您阅读[分布式计算的谬论](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing)。

&emsp;&emsp;现在让我们一起继续深入容器网络.
