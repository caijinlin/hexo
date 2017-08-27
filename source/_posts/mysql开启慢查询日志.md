---
title: mysql开启慢查询日志
tags: []
date: 2015-12-01 08:00:00
---

#### 登陆mysql客户端

    mysql -uroot -p123456

#### 开启检查

    show variables like 'slow_query_log';

#### 相关配置

    show variables like '%log%';

#### 开启

     set global log_queries_not_using_indexes = on;

#### 时间

    show variables like 'long_query_time';

#### 开启慢查询日志

    set global slow_query_log = on;

#### 查找慢查询日志记录位置

    show variables like 'slow%';

#mysqldumpslow -t 3 /usr/local/var/mysql/caijinlindeMBP-slow.log

    log-slow-queries="/usr/local/val/log/mysql-slow.log"
    long_query_time = 4
    log-queries-not-using-indexes
