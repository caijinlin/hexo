---
title: php数组合并隐患
tags: []
date: 2015-11-17 08:00:00
---

基于php数组操作，最近遇到两个坑，记录在这里

<!-- more -->

之前做一个搜索功能的时候，有一个需求是希望加一个“-”选项，以便可以取消搜索项

#### 第一次的做法
``` php
    $arr = array_merge(array(' ' => "-"), $arr);
```
[why not recommend array_merge](http://stackoverflow.com/questions/3292044/php-merge-two-arrays-while-keeping-keys-instead-of-reindexing)

隐患： array_merge合并时会重新索引，最后导致搜索的时候匹配失败

#### 第二次的做法
``` php
    $arr = array(' ' => "-") + $arr;
```

隐患: 如果$arr不是数组，就会发生意料的隐患

#### 最终做法
``` php
    settype($a, 'array');
    $arr = array(' ' => "-") + $arr;
```

### 总结

小小的一个功能，如果不注意也会引发一些问题。
