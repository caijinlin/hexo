---
title: thinkphp的一些坑
tags: []
date: 2015-11-11 08:00:00
---

### 记录一下昨晚遇到的坑

在页面中使用加密函数加密id时，发现解密的时候不正确，原以为是加密函数或者解密函数的问题，但以前用的时候都没有问题，突然出现这个问题应该不是加密函数或者解密函数的问题。


#### 页面中是这样写的
``` php
    <a class="btn btn-default" href="__URL__/edit#!/{:encrypt_id($_one.id)}/step4" title="查看">
        <i class="gi gi-search"></i>&nbsp;预览
    </a>
```

#### 数据排查
``` php
    $_one.id也能读出数据
```


#### 解决问题
``` php
   页面中使用php时，函数中参数有 “.” 的话，thinkphp解析的时候加密错误，多么大的一个坑啊，改为$_one['id']就好
```
