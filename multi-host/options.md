# 3.2 多主机容器网络的选择

&emsp;&emsp;Docker本身提供对覆盖网络的支持（基于主机间的底层网络而创建分布式网络）以及第三方提供商的网络插件。

&emsp;&emsp;实践中有多种多主机容器网络方案可选，特别是在Kubernetes环境中。主要包括如下多主机网络方案：

## Fannel

&emsp;&emsp;[Flannel](https://coreos.com/flannel/docs/latest/)是由CoreOS公司主导的一个虚拟网络方案，flannel为每个主机分配一个子网。在Kubernetes的环境下的每一个pod都有一个唯一的，可路由的IP。flannel支持一系列后端，例如VXLAN，AWS VPC和UDP。Flannel的优势在于它减少了端口映射的复杂性。例如，Red Hat公司的[Project Atomic](http://www.projectatomic.io)就是使用的[Flannel](https://twitter.com/ProjectAtomic/status/591231934505873408)。

## Weave Net

&emsp;&emsp;Weaveworks公司的[Weave网络](https://www.weave.works)也是创建了一个虚拟网络，多个主机上的Docker容器连接到此虚拟网络。应用程序使用此虚拟网络就好像容器都链接到同一个网络中的交换机一样，不需要配置端口映射和链接。无论这些容器运行在哪里，Weave网络上的应用程序容器提供的服务都可以被外界所访问。

&emsp;&emsp;同样，现有的内部系统可以暴露应用容器不管他们在哪里。Weave可以穿越防火墙并且支持部分连接；流量可以被加密，允许主机通过不可信网络连接。您可以通过Alvaro Saurin的文章“[Automating Weave Deployment on Docker Hosts with Weave Discovery](https://www.weave.works/blog/automating-weave-discovery-docker/)”了解Weave的服务发现功能。

&emsp;&emsp;如果你想尝试一下Weave，可以看看它的[Katacoda场景](https://katacoda.com/courses/weave)。

## Calico

&emsp;&emsp;Metaswitch的Calico项目使用标准的IP路由(准确地说，是[RFC 1105](https://tools.ietf.org/html/rfc1105)中定义的标准边界网关协议（BGP） 以提供3层网络解决方案。相比之下，大多数其他网络解决方案通过将第2层流量封装到更高层协议中来构建覆盖网络。

&emsp;&emsp;Calico的主要操作模式是不需要进行数据包的封装与解封装，专为可控制数据中心中的物理网络的公司所设计。

&emsp;&emsp;另外相近的另外一个项目[Canal](https://github.com/projectcalico/canal)，它将Calico所具有的网络策略这一优势跟flannel的后端网络实现相结合。

## Open vSwitch

&emsp;&emsp;Open vSwitch是一款多层虚拟交换机，旨在通过编程扩展实现网络的自动化，同时支持标准管理接口和协议，如NetFlow，IPFIX，LACP和802.1ag。此外，它旨在支持跨多个物理服务器进行数据分发，目前用于Red Hat的Kubernetes发行版[OpenShift](https://www.openshift.org)中，同时也是Xen，KVM，Proxmox VE和VirtualBox中的默认的虚拟交换机。它也被集成到许多私有云系统中，例如OpenStack和oVirt。

## OpenVPN

&emsp;&emsp;OpenVPN允许您使用TLS创建虚拟专用网络（VPN)。这些VPN也可以用于在公共互联网上安全地连接容器。如果你想尝试基于Docker的设置，我建议您看一下DigitalOcean的“[如何在Ubuntu 14.04的Docker容器中运行OpenVPN](https://www.digitalocean.com/community/tutorials/how-to-run-openvpn-in-a-docker-container-on-ubuntu-14-04)”演练教程。
