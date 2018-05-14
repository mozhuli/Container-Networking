# 7.5 Kubernetes中的服务发现

&emsp;&emsp;现在让我们来谈谈如何在[Kubernetes中发现服务](https://kubernetes.io/docs/concepts/services-networking/service/#discovering-services)。从概念上讲，您可以使用以下两种内置发现机制之一：

- 通过环境变量（有限）

- [使用DNS](https://github.com/kubernetes/dns/blob/master/docs/specification.md)，如果已经安装了相应的DNS组件

## 基于环境变量的服务发现

&emsp;&emsp;对于基于环境变量的服务发现方法，一个简单的示例可能类似于以下示例代码：

```bash
$ kubectl run -it --rm jump --restart=Never \
--image=quay.io/mhausenblas/jump:v0.1 -- sh
If you don't see a command prompt, try pressing enter.
/ # env
HOSTNAME=jump
WEBSERVER_SERVICE_HOST=10.104.58.143 WEBSERVER_PORT=tcp://10.104.58.143:80 WEBSERVER_SERVICE_PORT=80 WEBSERVER_PORT_80_TCP_ADDR=10.104.58.143 WEBSERVER_PORT_80_TCP_PORT=80 WEBSERVER_PORT_80_TCP_PROTO=tcp WEBSERVER_PORT_80_TCP=tcp://10.104.58.143:80
...
```

&emsp;&emsp;环境变量WEBSERVER_XXX为您提供可用于连接服务的IP地址和端口。例如，您可以在jump容器中执行`curl 10.104.58.143`，您应该看到NGINX欢迎页面。

&emsp;&emsp;环境变量的方式虽然方便，但请注意，通过环境变量进行发现具有一个根本性缺陷：您希望发现的任何服务必须在要发现它的pod之前创建，否则环境变量将不会由Kubernetes填充。幸运的是存在更好的方法：DNS。

## 基于DNS的服务发现

&emsp;&emsp;将像example.com这样的完全合格的域名（[FQDN](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)）映射到IP地址（如123.4.5.66）是DNS设计的目标。

&emsp;&emsp;在自己开发Kubernetes发行版时，也就是将所有必需组件（如SDN或DNS等附加组件）自己组合起来，而不是使用来自[30多种认证了的Kubernetes产品](https://github.com/cncf/k8s-conformance)。值得考虑DNS解决方案有：CNCF的[CoreDNS]项目(https://coredns.io/plugins/kubernetes/)，功能较少的[kube-dns组件](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns)。

&emsp;&emsp;那么我们如何使用DNS在Kubernetes中进行服务发现呢？如果安装并启用了DNS组件，该DNS服务器在Kubernetes API上监视正在创建或删除的service，它为它观察的每个service创建一组DNS记录。

&emsp;&emsp;在下一个示例中，让我们使用上面的webserver服务，并假设它已在默认namespace中运行。对于此服务，应存在DNS记录webserver.default（FQDN为webserver.default.cluster.local）。

```bash
$ kubectl run -it --rm jump --restart=Never \ 
--image=quay.io/mhausenblas/jump:v0.1 -- sh
If you don't see a command prompt, try pressing enter. 
/ # curl webserver.default
<!DOCTYPE html>
<html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
        body {
            width: 35em;
            margin: 0 auto;
            font-family: Tahoma, Verdana, Arial, sans-serif;
}
    </style>
    </head>
    <body>
    <h1>Welcome to nginx!</h1>
    <p>If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.</p>
    <p>For online documentation and support please refer to
    <a href="http://nginx.org/">nginx.org</a>.<br/>
    Commercial support is available at
    <a href="http://nginx.com/">nginx.com</a>.</p>
<p><em>Thank you for using nginx.</em></p> </body>
</html>
```

&emsp;&emsp;同一namespace中的Pod可以通过其短名称webserver访问该服务，而其他namespace中的Pod必须将该名称限定为webserver.default。请注意，这些FQDN查找的结果是ClusterIP。此外，Kubernetes支持命名端口的DNS服务（SRV）记录。因此，如果我们的Webserver具有名为http协议类型为TCP的端口，则可以从同一namespace为_http._tcp.webserver发出DNS SRV查询以发现http的端口号。还要注意，service的虚拟IP是稳定的，所以DNS结果不需要被重新查询。