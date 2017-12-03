---
title: dockeker中的Namespace
tags: ['namespace']
date: 2017-11-26 17:16:01
categories: cloud
---

最近开始研究docker与k8s部署相关的知识。k8s是容器编排工具，docker又是主流容器，其中docker底层采用了NAMESACE来做资源隔离，用CGROUP来控制资源的控制，还有docker是用GO语言写的，看来要学习的地方还有很多。

NAMESPACE主要是docker用来做容器的资源隔离。对系统的主机名，域名，IPC，PID，网络，文件系统，用户与用户组做资源隔离。与fork一个进程类似，但是其中涉及的方面更加细，更加广。


相关阅读：

[Docker背后的内核知识——Namespace资源隔离](http://www.infoq.com/cn/articles/docker-kernel-knowledge-namespace-resource-isolation?utm_source=infoq&utm_campaign=user_page&utm_medium=link "http://www.infoq.com/cn/articles/docker-kernel-knowledge-namespace-resource-isolation?utm_source=infoq&utm_campaign=user_page&utm_medium=link")

[docker 官方文档](https://docs.docker.com "https://docs.docker.com")

