---
title: mysql-optimization
date: 2017-06-05 21:26:44
tags: [mysql]
categories: 技术
---

### mysql优化实战攻略

最近对数据库查询进行了一些优化策略，总结如下：

### 加索引

`最简单的方法就是加索引，合适且必要才加，而不是乱加，数据量达到几十万以上效果明显。`

### 使用强制索引

`程序中使用强制索引，解决数据库没有按照我们想要的索引进行查询，百万级数据，效果显著。`

### 使用小表作为主表

`join查询的时候，数据量小的表作为主表，数据量大的表作为join的对象，也是一种不错的方法，减少全表扫描行数。`

### 数据冗余

`针对复杂的sql，需要join其它表且需要排序的情况下，可以挖掘统计数据，冗余表或者冗余字段。`


