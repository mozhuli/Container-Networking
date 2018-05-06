# 5.3 负载均衡

&emsp;&emsp;与服务发现密切相关的主题是负载均衡。通过负载均衡，您可以将负载（即入站服务请求）分散到多个容器中。在容器和微服务的环境中，负载平衡同时实现了几件事情：

- 它可以使吞吐量最大化并缩短响应时间。

- 它可以避免热点（即一个工作的容器过载）。

- 它可以帮助过度激进的DNS缓存，例如Java中的缓存。

&emsp;&emsp;下面按照字母顺序列出了容器环境下流行的负载平衡方案：

- [Bamboo](https://github.com/QubitProducts/bamboo)

    &emsp;&emsp;守护进程自动配置HAProxy实例，部署在Apache Mesos和Marathon上。 请参阅p24e指南“[Service Discovery with Marathon, Bamboo and HAProxy](http://programmableinfrastructure.com/guides/service-discovery/bamboo-haproxy-marathon/)”了解具体的配置。

- [Envoy](https://www.envoyproxy.io)

    &emsp;&emsp;以C++编写的高性能分布式代理，最初是在Lyft中构建的。Envoy旨在用于单一服务和应用程序，并为服务网格提供通信总线和数据平面。这是[Istio](https://istio.io)的默认数据平面。

- [Haproxy](http://www.haproxy.org)

    &emsp;&emsp;稳定，成熟，经过生产检验的负责均衡解决方案。通常与NGINX一起使用。

- [kube-proxy](https://kubernetes.io/docs/reference/generated/kube-proxy/)

    &emsp;&emsp;在Kubernetes集群的每个节点上运行并更新服务IP。它支持简单的TCP/UDP转发和round-robin负载均衡。请注意，它仅用于集群内部的负载均衡，并且还用作服务发现的支持组件。

- [Metallb](https://metallb.universe.tf)

    &emsp;&emsp;针对裸金属Kubernetes集群的负载均衡实现，解决了Kubernetes不提供此类集群默认实现的事实。换句话说，您需要进入公共云环境才能从此功能中受益。请注意，为了使MetalLB能够工作，您可能需要一个或多个支持BGP协议的路由器。

- [nginx](https://www.nginx.com/resources/admin-guide/load-balancer/)

    &emsp;&emsp;这个领域的领先解决方案。借助NGINX，您可以获得循环，最少连接和ip散列等负载均衡策略的支持，以及即时配置，监控和许多其他重要功能。

- [servicerouter.py](https://github.com/mesosphere/marathon-lb)

    &emsp;&emsp;一个简单的脚本，用于从Marathon获取应用程序配置并更新HAProxy; 请参阅p24e指南“[Service Discovery with Marathon, Bamboo and HAProxy](http://programmableinfrastructure.com/guides/service-discovery/bamboo-haproxy-marathon/)”

- [traefik](https://traefik.io)

    &emsp;&emsp;这一类的后起之秀。Emile Vauge（traefik的首席开发人员）一定在做正确的事情。我非常喜欢它，因为它就像HAProxy一样，默认支持一些后端，如Marathon和Consul，开箱即用。

- [Vamp-router](https://github.com/magneticio/vamp-router)

    &emsp;&emsp;受Bamboo和Consul-HAProxy的启发，Magnetic.io写了Vamp-router，它支持通过REST API或ZooKeeper更新配置，路由和过滤器用于Canary发布和A/B测试以及ACL，并提供统计信息。

- [Vulcand](http://vulcand.readthedocs.io/en/latest/)

    &emsp;&emsp;受[Hystrix](https://github.com/Netflix/Hystrix)启发的HTTP API管理和微服务的反向代理。

&emsp;&emsp;如果您想了解更多关于负载均衡的信息，请查看Kevin Reedy在[nginx.conf 2014关于NGINX和Consul上的负载均衡的演讲](https://www.youtube.com/watch?v=A2NOziRYh7U)。