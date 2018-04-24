# 2.3 网络管理考量

&emsp;&emsp;现在我们将从网络管理角度简要讨论您应该注意的一些方面。大多数这些问题对于多主机部署同样重要：

- IP地址分配

    &emsp;&emsp;当容器频繁创建、销毁时候，手动分配IP地址是不可持续的，桥接模式在一定程度上解决了这个问题。为了防止本地网络上的ARP冲突，Docker守护程序从分配的IP地址生成一个MAC地址。

- 管理端口

    &emsp;&emsp;有两种管理端口的方法：固定端口分配或端口动态分配。对于桥接模式，Docker可以自动分配（UDP或TCP）端口，从而使其可路由。像Kubernetes这样的系统采用扁平的IP容器网络模式，不会遇到这个问题。

- 网络安全

    &emsp;&emsp;开箱即用，Docker启用了[容器间通信](https://docs.docker.com/network/)（意味着缺省值为--icc=true）。这意味着主机上的容器可以互相通信而没有任何限制，这可能会导致拒绝服务攻击。此外，Docker通过--ip_forward和--iptables标志来控制容器间和容器与容器外的通信。一种好的做法是，您应该研究这些标志的默认设置，根据公司的实际安全策略在Docker守护程序中设置它们。

    &emsp;&emsp;像[CRI-O](http://cri-o.io)这样的系统，使用的是容器运行时接口（CRI），没有像Docker这样有功能庞大的守护进程，像较于Docker，可能会暴露更小的攻击面。

    &emsp;&emsp;另一个网络安全方面是线上加密，通常意味着[RFC 5246](https://tools.ietf.org/html/rfc5246)标准的TLS/SSL。
