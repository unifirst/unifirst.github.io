---
layout: post
title: "Intellij idea 中启动多个tomcat server失败问题解决"
date: 2016-03-10 21:32:08 +0800
comments: true
categories: [intellij idea, tomcat, war explored]
tags: [intellij idea, tomcat, war explored]
keywords: intellij idea, tomcat, war explored
description: Intellij idea 中启动多个tomcat server失败问题解决
---

如我在[由eclipse转intellij Idea](http://unifirst.github.io/blog/2016/02/29/eclipse-to-idea/)中提到，由于由Eclipse刚投入Intellij的怀抱不久，对一些使用尚不熟悉，尤其这两天在Intellij中配置启动多个Tomcat出现了问题。

###问题描述
Intellij idea中，为在本地调试两个系统之间的调用，配置两个本地tomcat server，设置不同的端口号，如8081和8082，Deploy中加入两个系统各自的Artifact xxx:war, Application context设置为“/“，即访问地址分别为http://localhost:8081/ 和 http://localhost:8082/ 。

问题来了，分别单独启动两个server时都能成功；但是同时启动两个系统时，两个系统都会出现问题。其中较先启动的server报错为：StandardServer.await: Invalid command '' received，然后会有一个系统报出异常，提示找不到xml或者properties等。

<!-- more -->

###寻求解决方法
报出的找不到xml或properties等异常，肯定是误报，因为单独启动时是没有问题的。

根据StandardServer.await: Invalid command '' received百度或者google，得到的结果基本是端口的问题。但是我已经配置了不同的端口号，除上述的http port外，我还查看了server.xml中的shut down port、ajp port等等，均不相同。大略可以排除端口号的问题。

请教同事，同事解释Application context不能同为"/"，Intellij会将web发布到tomcat目录下的ROOT中，两者必然冲突。提供了两种解决方案：

 1. Application context区别开，如"/weba/"和"/webb/"
 2. 将tomcat安装目录复制一份，用两套tomcat部署

我恍然同时，又觉得Eclipse完全可以实现啊，Intellij这都实现不了是不是有点low了。

###问题解决
最终的最终，我发现了问题所在。在Deploy中加入的Artifact不应该是war，而应该选择第二种war explored！

搜索了war和war explored的区别。网上大都在讨论两者最大的区别是explored支持热加载，方便本地修改调试。但是针对本文的问题，没有找到直接解释。

自己浅析一下：war理所当然会打为war包，发布时候脱离了你本地项目目录，发布到了Tomcat目录\webapps\ROOT下；explored方式，是将web root指向了你的本地项目。因此war形式会产生冲突，而explored方式不会，且explored方式可以热加载。