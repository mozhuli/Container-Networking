# 7.3 Pod内网络

&emsp;&emsp;在一个pod内有一个所谓的基础设施容器（pause container）。这是kubelet启动的第一个容器，它获取Pod的IP并设置网络命名空间。然后，该pod中的所有其他容器将加入到pause容器的网络和IPC命名空间。infra容器启用桥接网络模式，并且该pod中的所有其他容器都通过容器模式加入pause容器的网络命令空间。在pause容器中运行的初始过程没有任何其他作用，除了提供命名空间给其他容器共享。如果pause容器退出，则Kubelet杀死pod中的所有容器，然后开始清理工作。

&emsp;&emsp;由于以上原因，一个pod中的所有容器都可以使用localhost（或IPv4中的127.0.0.1）相互通信。您自己负责确保pod中的容器在使用的端口方面不会相互冲突。还要注意，这也意味着减少了pod内容器之间的隔离; 然而，此处pod紧密耦合的设计在容器编排环境中是一种很好的设计。

&emsp;&emsp;如果您想了解更多关于pause容器的信息，请阅读Ian Lewis的[The Almighty Pause Container](https://www.ianlewis.org/en/almighty-pause-container)。
