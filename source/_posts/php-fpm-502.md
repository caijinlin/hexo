---
title: php-fpm监听进程不存在
tags: []
date: 2015-11-18 08:00:00
---

基于lnmp安装的php-fpm启动后，发现并没有看到9000进程，加了网站配置文件后，出现502错误。

php-fpm可以正常启动，php-fpm默认在9000端口监听, 但是netstat并没有看到9000进程

#### 启动查找进程
``` php
    /etc/init.d/php-fpm start
    netstat -anp | grep 9000
```

#### 查看php-fpm配置文件
``` php
    vim /usr/local/php/etc/php-fpm.conf
    [global]
    pid = /usr/local/php/var/run/php-fpm.pid
    error_log = /usr/local/php/var/log/php-fpm.log
    log_level = notice

    [www]
    listen = /tmp/php-cgi.sock  #监听，改成127.0.0.1:9000
    listen.backlog = -1
    listen.allowed_clients = 127.0.0.1
    listen.owner = www
    listen.group = www
    listen.mode = 0666
    user = www
    group = www
    pm = dynamic
    pm.max_children = 10
    pm.start_servers = 2
    pm.min_spare_servers = 1
    pm.max_spare_servers = 6
    request_terminate_timeout = 100
    request_slowlog_timeout = 0
    slowlog = var/log/slow.log

```

#### 网站配置文件test.com.conf
``` php
    server {
        listen 80;
        server_name test.com;
        index index.html index.shtml index.php;
        root /home/wwwroot/default/test;
        include /home/wwwroot/default/test/nginx_rewrite.conf;
        location ~ .*\.(php|php5)?$
        {
            fastcgi_pass 127.0.0.1:9000; #9000端口
            fastcgi_index index.php;
            include fastcgi.conf;
        }
        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf|woff)$
        {
            expires 30d;
            access_log        off;
            log_not_found     off;
        }
        location ~ .*\.(js|css)?$
        {
            expires 7d;
            access_log        off;
            log_not_found     off;
        }
        location ~ .*\.(htaccess)?$
        {
            deny all;
        }
    }
```

### 对比php-fpm.conf与test.com.conf发现php-fpm的监听和fastcgi_pass不太一样

```php
    两者需要将监听形式改成一样，比如都是127.0.0.1:9000或者/tmp/php-cgi.sock
```
