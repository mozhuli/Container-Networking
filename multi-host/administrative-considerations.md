# 3.4 网络管理考量

&emsp;&emsp;在本章的最后一节中，我们将讨论您应该注意的一些网络管理方面的问题：

## IPVLAN

&emsp;&emsp;Linux内核版本[3.19](https://kernelnewbies.org/Linux_3.19)引入了IP-per-container功能。这为主机上的每个容器分配一个唯一且可路由的IP地址。IPVLAN使用单个的网络接口同时创建多个具有不同MAC地址的虚拟网络接口。

&emsp;&emsp;这项由Google的Mahesh Bandewar提供的[内核功能](https://github.com/torvalds/linux/blob/master/Documentation/networking/ipvlan.txt)在概念上类似于[macvlan驱动程序](http://backreference.org/2014/03/20/some-notes-on-macvlanmacvtap/)，但IPVLAN更灵活，因为它在L2和L3上运行。 注意：此功能只支持Linux内核版本>3.19的内核。

## IP地址管理（IPAM）

&emsp;&emsp;多主机网络的关键挑战之一是如何将IP地址分配给集群中的每一个容器。有两种策略：1. 在现有的网络中找到实现它的方法；2. 跟现有网路正交，也就是实际上隐藏的网络层（即覆盖网络）。请注意，对于IPv6，第一种策略很轻松可以实现，因为找到一个空闲的地址空间应该容易得多。

## 编排工具兼容

&emsp;&emsp;本章讨论的许多多主机网络解决方案都是需要多组件的协同工作，包装Docker API并为您配置网络。所以在您选择具体网络方案之前，您应该确保检查您使用的容器编排工具是否存在任何兼容性的问题。在第4章中我们将详细谈论此类问题。

## IPv4 vs IPv6

&emsp;&emsp;到目前为止，大多数Docker部署都使用标准的IPv4，但IPv6有一定的吸引力。自2015年2月发布v1.5以来，Docker已经支持IPv6; 然而，Kubernetes的IPv6支持尚未完成。IPv4不断增长的地址短缺问题可能会鼓励更多的IPv6部署，也会摆脱网络地址转换（NAT），但尚不清楚究竟何时会达到临界点。
