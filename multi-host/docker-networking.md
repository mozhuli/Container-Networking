# 3.3 Docker网络

&emsp;&emsp;在Docker 1.9版本引入了一个新的[docker network命令](https://blog.docker.com/2015/11/docker-multi-host-networking-ga/)。有了这个命令，Docker容器可以动态地连接到其他网络，每个网络可能由不同的网络驱动程序支持。
2015年3月，Docker Inc.[收购](https://www.networkworld.com/article/2893325/sdn/docker-buys-sdn-start-up-for-container-networking.html)了SDN创业公司SocketPlane，并将其产品重新命名为[Overlay Driver](https://blog.docker.com/2015/06/networking-receives-an-upgrade/)。自从Docker 1.9以来，这是多主机网络的默认设置。Overlay Driver通过[点对点通信](https://www.serf.io)扩展了常规网桥模式，并使用可插拔的键值存储后端来存储群集的状态信息，支持Consul，etcd和ZooKeeper。

&emsp;&emsp;要了解更多信息，我建议阅读以下博客文章：

- Aleksandr Tarasov的“[容器网络的辉煌与衰败](http://developerblog.info/2015/11/16/splendors-and-miseries-of-docker-network/)”

- Project Calico的“[Docker 1.9 Includes Network Plugin Support and Calico Is Ready!](https://www.projectcalico.org/docker-libnetwork-is-almost-here-and-calico-is-ready/)”

- Weaveworks的“[Life and Docker Networking – One Year On](https://www.weave.works/blog/docker-networking-1-9-weave-plugin/)”