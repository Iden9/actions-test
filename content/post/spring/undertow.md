---
title: undertow 替换 tomcat
date: 2024-10-27
categories: ["java","springboot"]
---

## 大公司为什么禁止SpringBoot项目使用Tomcat？


### 前言
在SpringBoot框架中，我们使用最多的是Tomcat，这是SpringBoot默认的容器技术，而且是内嵌式的Tomcat。同时，SpringBoot也支持Undertow容器，我们可以很方便的用Undertow替换Tomcat，而Undertow的性能和内存使用方面都优于Tomcat，那我们如何使用Undertow技术呢？本文将为大家细细讲解。

SpringBoot中的Tomcat容器
SpringBoot可以说是目前最火的Java Web框架了。它将开发者从繁重的xml解救了出来，让开发者在几分钟内就可以创建一个完整的Web服务，极大的提高了开发者的工作效率。Web容器技术是Web项目必不可少的组成部分，因为任Web项目都要借助容器技术来运行起来。在SpringBoot框架中，我们使用最多的是Tomcat，这是SpringBoot默认的容器技术，而且是内嵌式的Tomcat。


SpringBoot设置Undertow
对于Tomcat技术，Java程序员应该都非常熟悉，它是Web应用最常用的容器技术。我们最早的开发的项目基本都是部署在Tomcat下运行，那除了Tomcat容器，SpringBoot中我们还可以使用什么容器技术呢？没错，就是题目中的Undertow容器技术。SrpingBoot已经完全继承了Undertow技术，我们只需要引入Undertow的依赖即可，如下图所示。

图片
图片
配置好以后，我们启动应用程序，发现容器已经替换为Undertow。

那我们为什么需要替换Tomcat为Undertow技术呢？

Tomcat与Undertow的优劣对比
Tomcat是Apache基金下的一个轻量级的Servlet容器，支持Servlet和JSP。Tomcat具有Web服务器特有的功能，包括 Tomcat管理和控制平台、安全局管理和Tomcat阀等。Tomcat本身包含了HTTP服务器，因此也可以视作单独的Web服务器。但是，Tomcat和ApacheHTTP服务器不是一个东西，ApacheHTTP服务器是用C语言实现的HTTP Web服务器。Tomcat是完全免费的，深受开发者的喜爱。

图片
Undertow是Red Hat公司的开源产品, 它完全采用Java语言开发，是一款灵活的高性能Web服务器，支持阻塞IO和非阻塞IO。由于Undertow采用Java语言开发，可以直接嵌入到Java项目中使用。同时， Undertow完全支持Servlet和Web Socket，在高并发情况下表现非常出色。

图片
我们在相同机器配置下压测Tomcat和Undertow，得到的测试结果如下所示：

QPS测试结果对比：
Tomcat
图片
Undertow
图片
内存使用对比：
Tomcat
图片
Undertow
图片
通过测试发现，在高并发系统中，Tomcat相对来说比较弱。在相同的机器配置下，模拟相等的请求数，Undertow在性能和内存使用方面都是最优的。并且Undertow新版本默认使用持久连接，这将会进一步提高它的并发吞吐能力。所以，如果是高并发的业务系统，Undertow是最佳选择。

最后
SpingBoot中我们既可以使用Tomcat作为Http服务，也可以用Undertow来代替。Undertow在高并发业务场景中，性能优于Tomcat。所以，如果我们的系统是高并发请求，不妨使用一下Undertow，你会发现你的系统性能会得到很大的提升。