---
layout: post
title: "由eclipse转intellij idea"
date: 2016-02-29 17:34:20 +0800
comments: true
categories: intellij idea
---
###设置字符集utf8
依次打开 File | Settings | Editor | File Encodings，将IDE Encoding、Project encoding 、default encoding for properties, 均选择utf8

###设置unix换行符
依次打开 File | Settings | Editor | Code Style，将Line separator (for new  files) 选择 Unix and OS X(\n)

同时可以设置行宽：Right margin (columns): 120

###快捷键设置
关于idea的快捷键，一搜一堆，不多说。

主要的对应关系：（eclipse ——	intellij）

	ctrl+shift+R —— ctrl+shift+n
	ctrl+shift+T —— ctrl+n
	alt+← —— ctrl+alt+←
	F3（ctrl+left button） —— ctrl+B（ctrl+left button）
	Ctrl+D —— Ctrl+Y
	Alt+Shift+Up/Down —— Ctrl+D
	Ctrl+Shift+F —— Ctrl+Alt+L
	Ctrl+Shift+O —— Ctrl+Alt+O
	……

在File | Settings | Keymap 中，可以选择eclipse、vs等风格的快捷键

###设置主题、字体
在File | Settings | Appearance & Behavior | Appearance 设置界面窗口的主题、字体大小

在 File | Settings | Editor | Colors & Fonts | Font 设置编辑区的主题、字体大小。需要注意，原主题无法修改，需要save as建立自己的主题，然后才允许修改

###console / terminal
这是intellij中很棒的功能。alt+ F12即可打开，可以执行系统的命令。如git、mvn、java等。

###git使用
eclipse中是在右键team中进行git的操作。intellij中，也可右键选择git对文件进行git操作，如revert（类似于eclipse中的overwrite）等。

intellij中，最爽的就是可以直接打开console执行git命令了。当然也可以通过git bash单独打开。在console中，试着多用git的命令吧。

###maven使用
公司的项目，一般都是在maven安装目录中，单独设置了setting.xml。刚刚open一个公司的项目时，总会一堆编译错误。其实不外乎两步解决：

1. 依次打开 File | Settings | Build, Execution, Deployment | Build Tools | Maven, 将Maven home directory设置为maven的安装目录，以便使用之前已弄好的setting.xml
2. 选择project或者pom.xml，右键maven中选择Reimport，一般就OK啦

其它的maven操作暂未用到，若需要，mvn命令想来也很方便。

###tomcat server
依次打开Run | Edit configurations, 点击“+”号，在列表中选择Tomcat server -> local, Server标签下起好Name、配好port，Deployment标签下“+”入artifacts就完成了。

上述添加完后，就可以run或者debug了。

###导入Eclipse的代码格式化文件
插件Eclipse Code Formatter可以完成这个任务。

File | Settings | Plugins中搜索Eclipse Code Formatter，然后install。然后就可以看到File | Settings | Other Settings | Eclipse Code Formatter了，里面选择Use the eclipse code formatter, 然后在Eclipse Java Formatter config file中选择自己的formatter xml文件就完成了。

在文件中，Ctrl+alt+L就可以format代码了。

其实eclipse还有个文件，就是code template，定义comment格式的。这个暂时还未找到导入方案……