---
title: redis read error on connection
tags: []
date: 2015-10-10 08:00:00
---

### 简单缓存服务SCS

高性能、高可用的分布式缓存服务，兼容Memcache/Redis协议。

#### 使用SCS中的redis时, 遇到"redis read error on connection"的错误， 经过一番搜索找到解决方法。

登录百度云后台，需将访问改集群的服务器设置为白名单

    简单缓存服务SCS => 集群名称 => 添加白名单 =》 选择服务器
