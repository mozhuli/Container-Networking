# 7.7 Kubernetes 中网络的高级主题

&emsp;&emsp;下面我将介绍两个与Kubernetes网络相关的高级主题：网络策略和服务网格。

## Network Policies

&emsp;&emsp;Kubernetes中的[网络策略](https://kubernetes.io/docs/concepts/services-networking/network-policies/)允许您指定如何允许pod间彼此进行通信。Kubernetes 1.7及以上版本的网络策略被认为是稳定的，因此您可以在生产中使用它们。

&emsp;&emsp;我们来看看具体的一个例子。例如，假设您想禁止所有通往superprivate namespace中所有pod的流量。您可以为该namespace创建默认的Egress策略，如下例所示：

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
    name: bydefaultnoegress
    namespace: superprivate
spec:
    podSelector: {}
    policyTypes:
    - Egress
```

&emsp;&emsp;请注意，不同的Kubernetes发行版在不同程度上支持网络策略：例如，在OpenShift中，它们作为一等公民受到支持，并且可以通过[redhat-cop/openshitoolkit](https://github.com/redhat-cop/openshift-toolkit/tree/master/networkpolicy) 找到一系列的示例。

&emsp;&emsp;如果您想了解更多关于如何使用网络策略的信息，请查看Ahmet Alp Balkan的实用且详尽的博客“[Securing Kubernetes Cluster Networking](https://ahmet.im/blog/kubernetes-network-policy/)”.

## Service Meshes

&emsp;&emsp;展望未来，您可以使用服务网格，例如下面所要讨论的两款服务网格方案。服务网格的想法是，开发人员不必把网络通信和控制的负担放到自己身上，而是将这些工作外包给服务网格。因此，您可以从流量控制，可观察性，安全性等方面受益，而无需对源代码进行任何的更改。是不是特别棒？

### Istio

&emsp;&emsp;[Istio](https://istio.io)是目前最流行的服务网格，可用于Kubernetes，但不完全如此。它使用Envoy作为默认数据平面，它自己主要侧重于控制平面方面。仅举几例功能，它支持监视（Prometheus），跟踪（Zipkin/Jaeger），断路器，路由，负载平衡，故障注入，重试，超时，镜像，访问控制和速率限制等。Istio需要将Envoy代理作为sidecar容器部署在您的pod中。你可以通过Christian Posta的文章了解更多关于Istio的信息：[Deep Dive Envoy and Istio Workshop](http://blog.christianposta.com/microservices/deep-dive-envoy-and-istio-workshop/)。

### Conduit

&emsp;&emsp;[Conduit](https://conduit.io)由作为数据平面（由Rust编写）的sidecar容器和管理这些代理的控制平面（用Go编写）组成，类似于Istio。在CNCF项目[Linkerd]之后，这是Buoyant关于服务网格思想的第二次迭代; 他们是这个领域的先锋，且在2016年建立了服务网格概念。通过Abhishek Tiwari的博客文章“[Getting started with Con‐ duit - lightweight service mesh for Kubernetes](https://abhishek-tiwari.com/getting-started-with-conduit-lightweight-service-mesh-for-kubernetes/)”了解更多信息。

&emsp;&emsp;在我们结束本章和本书之前还有一点需要注意：服务网格还是很新的，所以你将其用于生产环境之前三思而行。