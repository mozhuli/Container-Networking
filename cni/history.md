# 6.1 历史

&emsp;&emsp;CNI是CoreOS在它的容器运行时rkt环境中率先开发的，用于定义网络插件，容器运行时和编排系统之间的通用接口。[Docker最初计划支持它](https://github.com/containerd/containerd/issues/362)，但随后提出了Docker专有的[libnetwork](https://github.com/docker/libnetwork)方法来实现容器网络连接。

&emsp;&emsp;CNI和libnetwork是在2015年4月至6月期间并行开发的，经过一番讨论后，Kubernetes社区决定[不采用libnetwork](https://kubernetes.io/blog/2016/01/why-kubernetes-doesnt-use-libnetwork)，而是使用CNI。现在几乎所有除Docker Swarm之外的容器编排系统都使用CNI; 所有容器运行时都支持它，并且支持CNI标准的插件很多。

&emsp;&emsp;2017年5月，[CNCF接受CNI成为其下的一个顶级项目](https://containerjournal.com/2017/05/23/cncf-aims-make-container-network-interface-standard/)。