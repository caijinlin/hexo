---
title: php细节整理
tags: []
date: 2015-04-08 08:00:00
---

### php一些注意的点

最近在php开发时，发现业务多了，经常会遇见因为php细节注意不当而导致的bug，影响开发效率，记录在这里。

<!-- more -->

php作为一种弱类型语言，所以强制类型转化有时就变得特别重要

#### 判断某个变量是否存在建议用isset,即使$a等于0也不会有问题
``` php
    if (isset($a)) {            if ($a) {
                        not=》
    }                           }
```
#### define常量时，判断一下
``` php
    !defined('PROJECT_ID') && defined('PROJECT_ID', 2);
    如果PROJECT_ID没有定义时，输出PROJECT_ID ,则会打印出"PROJECT_ID"字符串，
    所以使用的时候需要(int) PROJECT_ID判断下，是否存在。
```

#### 不需要使用的变量，尽量unset，节约内存
``` php
    unset($a);
```

#### 在某些情况下，你可以使用isset() 技巧加速执行你的代码。
```
（举例如下） if (strlen($foo) < 5) { echo 'Foo is too short'; } 
（与下面的技巧做比较） if (!isset($foo[5])) { echo 'Foo is too short'; } 
```
调用isset()恰巧比strlen()快，因为与后者不同的是，isset()作为一种语言结构，意味着它的执行不需要函数查找和字母小写化。

#### 总结

很多php细节需要注意，一直在路上！

