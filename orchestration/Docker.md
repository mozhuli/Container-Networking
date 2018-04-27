# 4.2 Docker

&emsp;&emsp;在编写本文时，Docker在分布式环境中使用所谓的swarm模式，而在Docker 1.12之前，使用了独立的Docker Swarm模型。我们将在这里进行讨论。

## Swarm模式

&emsp;&emsp;自Docker 1.12以来，[swarm模式](https://docs.docker.com/engine/swarm/)已与Docker Engine集成。嵌入在Docker Engine中的编排功能是使用[SwarmKit](https://github.com/docker/swarmkit/)构建的。

&emsp;&emsp;Docker中的Swarm由多个运行在swarm模式下的主机组成，充当manager和worker角色（主机可以是manager，worker或同时充当这两种角色）。想对于独立的容器，任务就是一个正在运行的容器，它是swarm服务的一部分，由swarm manager进行管理。Docker swarm模式中的服务定义为要在manager或worker上执行的任务。Docker的工作内容是维持所期望的状态; 例如，如果一个工作节点变得不可用，Docker会将这些任务调度到另一个主机上。

&emsp;&emsp;以swarm模式运行的Docker不会阻止您在组成群集的任何主机上运行独立的容器。独立容器和群集服务之间的本质区别是，只有群集管理员可以管理群集，而独立容器可以在任何主机上启动。

&emsp;&emsp;要详细了解Docker的swarm模式，请查看官方的“[Swarm模式入门](https://docs.docker.com/engine/swarm/swarm-tutorial/)”教程或在Katacoda上的“[Docker Orchestration - Swarm模式入门](https://katacoda.com/courses/docker/getting-started-with-swarm-mode)”在线进行实践。

## Docker Swarm

&emsp;&emsp;Docker历史上有一个名为[Docker Swarm](https://docs.docker.com/swarm/)的本地集群管理工具。Docker Swarm[基于Docker API构建的](https://www.slideshare.net/Docker/2015-dockercon-orchestrationsysadmins)，其工作方式如下：有一个Swarm manager负责调度，以及负责本地资源管理的代理运行的每个主机上（图4-3）。

![图4-3 Docker Swarm架构，基于T-Labs演示[PPT](https://www.slideshare.net/snrism/swarm-container-cluster-service)](../images/4-3.png)

&emsp;&emsp;Docker Swarm支持不同的[存储后端](https://docs.docker.com/swarm/discovery/)：etcd，Consul和ZooKeeper。您还可以使用静态文件通过Swarm捕获您的群集状态，最近引入了一个名为[wagl](http://ahmetb.github.io/wagl/)的基于DNS的Swarm服务发现工具。