---
layout: post
title: "count(*)，count(1)和count(field)区别"
date: 2016-02-16 17:39:14 +0800
comments: true
categories: mysql
---

印象中，count(key)比count(\*)效率要高，因此在项目中用了count(field)的形式来统计行数。在code reivew时被指出应用count(\*)，于是查了下，并做了下简单测试，果然是我记错了，足见code review是多么有用啊。

### count(\*)

count(\*)是对不为null的行进行计数，因此某一行只要不是所有列都为null（即只要是存在的记录），就会被计数。

mysql用explain查看其执行计划，count(\*)会尽量利用具有以下特征的索引来提高性能：

 1. not null列
 2. 字段较窄

![explain查看count(\*)执行计划](http://img.blog.csdn.net/20160216181909126)
如图所示，表主键id为bigint类型，count(\*)时自动选择了int类型的gst_id索引。

### count(field)

count(field)是对field列不为null的行进行统计，因此某一行的该列为null，则不予计数 。

同样用explain查看其执行计划，count(field)同样会尽量利用索引来提高性能，暂时发现有以下两种情况：

 1. 含有该field的索引
 2. 若改field为主键，则同count(\*)一样，会选择更窄的索引，此时和使用count(\*)无异

由此可见，用count(field)来进行统计会有以下问题：

 1. 若该field有null记录，意图用来统计所有记录时，结果是错误的
 2. 若该field没有索引或者不是最优索引，则效率会低

### count(1)

还见到count(1)用法。mysql中验证没有发现与count(\*)明显区别，暂且认为是一样的。

###小结

count(\*)和count(1)无太大差别，count(field)若使用不当会带来错误或性能问题，不建议使用。

另外，若含有where语句，则会优先where中条件索引，上面讨论的执行计划，应该没多大意义了。