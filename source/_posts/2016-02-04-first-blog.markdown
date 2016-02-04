---
layout: post
title: "博客建立之路"
date: 2016-02-04 12:17:12 +0800
comments: true
categories: 
---
##blog历程
### 托管博客
我先后用过[新浪博客](http://blog.sina.com.cn/heiflow)、[CSDN博客](http://blog.csdn.net/unifirst)、[博客大巴](http://zhendexiangxxzhegeblogziyuming.blogbus.com/)还有其它一些不知名的小blog，当然还有QQ空间、校内等。每次想记些东西的时候，总是纠结于要记录在哪。久而久之，貌似处处都有blog，然而又处处不长久。<br />
印象尤为深刻的，是以前选了一个很冷门的blog网站，自己偏安一隅地写着blog，结果有一天被通知网站要关闭了，之后export出来，我还用windows自带的加密给文件加了下密，还没来得及处理，后来的一次重装系统，再也无法解密了。

###自建blog
有追求的人都自己搭建blog，看网上很多wordpress的教程，也搞过。当时穷学生一个，舍不得花钱买空间、买域名，找免费的空间和域名（比如tk），到时也出来过博客首页，到最后都不了了之。

###github
毕业后进了国企，就再也没想过这档子事。两年后出来，感觉仿佛变了天，git？没用过啊。面试，还要最好有git的项目？瞬间感觉被落下好几个世纪。<br />
好在终于进了个不大不小的互联网公司，开始兢兢业业地向大家学习。也终于逐渐知道了github是怎么回事，而且竟然了解了通过git可以搭建blog，这让我跃跃欲试。

##github中博客的搭建
各种教程网上遍布，我也就不班门弄斧了。甚至看到了关于大家传播github搭建blog是否会导致github走向sourceforge命运的讨论。作为旁观者我就是看看，我不说话。<br />
首先是唐巧的两篇文章给了我很大启示[《象写程序一样写博客：搭建基于github的博客》](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/)和[《作为码农，我们为什么要写作》](http://blog.devtang.com/blog/2014/01/08/why-we-need-write/)给了我很大启示和帮助。我虽然年近30但事业上一事无成，但看过一篇鸡汤文章[《我说来不及，你就不学了吗](http://toutiao.com/a6240890766765506818/)》，告诉我任何时候开始都不算晚。<br />
在这春节前的最后一两个工作日，也终于算是稍有空闲。准备上手搭建这个blog。

###github
git的作用想必大家都了解，很强大的版本管理工具，其依托的github上可以实现项目的管理及分享，是码农们的圣殿。<br />
用github搭建blog，其实是用了其提供出来的个人page或者project的page，本意是用于界面化展示个人（或组织）信息或者项目信息的，由于其灵活的可管理定制能力，被大家钻空式地用在了blog上。

###octopress
只用github，就完全可以搭建blog了。但所有工作都自己来完成，总是有些许不便，也总有些极客极富兴趣地让一些事情变得简单，于是出现了类似于[octopress](http://octopress.org/)的工具。<br />
我搭建blog所有的过程，均效仿自octopress官网中的[Octopress Setup](http://octopress.org/docs/setup/)及[Deploying to Github Pages](http://octopress.org/docs/deploying/github/) 的部分。唐巧[《象写程序一样写博客：搭建基于github的博客》](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/)中似有不全。

###GitCafe
github搭建的blog在国内访问，速度的确令人拙计，唐巧的另一篇博客[《将博客从GitHub迁移到GitCafe》](http://blog.devtang.com/blog/2014/06/02/use-gitcafe-to-host-blog/)提供了一种全新的思路。“我强烈建议各位基于 Github Pages 功能来搭建个人博客的朋友，将博客内容镜像到 GitCafe 上”，让我知道我的博客以后的发展方向，目前想来没什么值得大家关注的内容，期待有足够大访问量让我后续有不断改进的动力。

###Markdown
估计不得不提的就是这个Markdown。百度百科:“Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。”<br />
我初次见到Markdown是在发布CSDN的blog时，这篇blog也正是用CSDN的来编写的。
看网上推荐，windows下最好用的是编辑软件是[markdownpad2](http://www.markdownpad.com/download.html)，已下载，还未安装试用。


##小结
总之，我的github的blog启动了。希望能通过它，让我不断积累，不断进步。<br />
以后，会陆续加Comments（如Disqus）、文章列表、Catagories等功能，若有需要，会加入Google Analytics及迁移GitCafe等。<br />
如今最重要的，是先用起来。