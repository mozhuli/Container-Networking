# 1.2 Go Cattle！

&emsp;&emsp;将“牲畜模式"应用于基础架构中的美妙之处在于，它允许您扩展硬件（甚至是异构硬件。 例如，请参见Thorvald Natvig在Velocity 2015上的演讲：[数据中心的具有挑战性的基本假设：从硬件解耦基础设施](https://conferences.oreilly.com/velocity/devops-web-performance-ny-2015/public/schedule/detail/43771)”。）

&emsp;&emsp;它为混合云带来了弹性。

&emsp;&emsp;最重要的是，从运维人员的角度来看，“牲畜模式"可以让您获得体面的夜间睡眠，因为您将不需要在凌晨3点进行分页，只是为了更换损坏的硬盘驱动器或在不同的服务器上重新启动挂起的应用程序就像“宠物模式"那样。

&emsp;&emsp;然而，“牲畜模式"带来了一些挑战：

- 非技术挑战
    
    &emsp;&emsp;我敢说大部分挑战都是非技术性的，我如何说服我的经理？ 我如何说服的CTO采取这种模式？ 我的同事们是否会反对这种新的做事方式？ 这是否意味着我们将需要更少的人来管理我们的基础设施？ 本书中我不会为这些问题提供现成的解决方案;  相反，你可以去购买由Gene Kim，Kevin Behr和George Spafford（O'Reilly）撰写的[The Phoenix Project](http://shop.oreilly.com/product/9780988262508.do)，它应该可以帮助你找到答案。

- 技术挑战
    
    &emsp;&emsp;技术挑战主要包括处理诸如机器的基本配置等问题，例如，使用Ansible来安装Kubernetes组件，如何建立容器之间和外部世界之间的通信链接，最重要的是，如何确保容器可自动部署和可发现的。

&emsp;&emsp;现在您已经了解“宠物模式” 与“牲畜模式"的异同，下节我将介绍整个容器网络技术栈。
