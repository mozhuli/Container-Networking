# 6.3 容器运行时和插件

&emsp;&emsp;CNI附带了许多[内置的插件](https://github.com/containernetworking/plugins)，例如loopback和vlan。还有很多可用的第三方CNI插件。以下是按字母顺序排列的比较常用的CNI插件：

- [Amazon ECS CNI插件集合](https://github.com/aws/amazon-ecs-cni-plugins)

    亚马逊ECS使用的CNI插件集合，用Elastic Network Interfaces（ENI）配置容器的网络命名空间。

- [Bonding](https://github.com/intel/bond-cni)

    英特尔开发的CNI插件，用于故障转移和云原生环境中构建高可用的网络。

- [Calico](https://github.com/projectcalico/calico-cni)

    Project Calico的CNI网络插件。Project Calico管理的是一个扁平的3层网络，为每个工作负载分配一个完全可路由的IP地址。对于需要覆盖网络的环境，Calico使用IP-in-IP隧道或可以与其他覆盖网络（[flannel](https://github.com/coreos/flannel)）一起使用。

- [Cilium](https://github.com/cilium/cilium)

    基于BPF的解决方案，提供容器之间的网络连接，可以在3/4层提供网络和安全的网络服务以及在7层提供HTTP和gRPC等现代协议。

- [CNI-Genie](https://github.com/Huawei-PaaS/CNI-Genie)

    华为的通用CNI网络插件。

- [Infoblox](https://github.com/infobloxopen/cni-infoblox)

    一个CNI的IPAM插件，与Infoblox接口配合提供IP地址管理服务。

- [Linen](https://github.com/John-Lin/linen-cni)

    基于Open vSwitch的覆盖网络CNI插件。

- [Multus](https://github.com/Intel-Corp/multus-cni)

    英特尔开发的支持多CNI插件的插件。

- [nuage](https://github.com/nuagenetworks/nuage-cni)

    支持Kubernetes的网络策略的Nuage Networks SDN插件。

- [Romana](https://github.com/romana/kube)

    支持Kubernetes网络策略的3层CNI插件。

- [Silk](https://github.com/cloudfoundry/silk)

    受flannel启发，专为Cloud Foundry设计的CNI插件，

- [Vhostuser](https://github.com/intel/vhost-user-net-plugin)

    该插件与Open vSwitch和[OpenStack VPP](https://github.com/openstack/networking-vpp)以及Kubernetes中的Multus CNI插件一起运行，主要用于裸机容器部署。

- [Weave](https://github.com/weaveworks/weave#weave-net)

    Weaveworks开发的CNI插件。