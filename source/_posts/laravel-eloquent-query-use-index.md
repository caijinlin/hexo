---
title: laravel-eloquent-query-use-index
date: 2017-05-31 21:12:38
tags: [laravel,mysql]
categories: 技术
---

#### 为什么需要强制索引？

`数据库没有使用我们设想的索引进行sql查询，导致查询特别慢。`

#### mysql强制索引查询语句

```sql
select * from test where tt = 1 force index(idx_tt); // 强制索引
select * from test where tt = 1 use index(idx_tt); // 优先按照这种索引查找
```

#### laravel中实现强制索引查询

```php
$this->model
->setTable(DB::connection('test_db')->raw('test' . ' FORCE INDEX(tt)'))
->where('tt', 1)
->get();
```
