---
title: centos搭建reviewboard
tags: []
date: 2015-02-15 08:00:00
---

### centos下搭建reviewboard

<!-- more -->

#### 安装apache,php,mysql,phpmyadmin,memcache

  yum install httpd
  yum install php
  yum -y install mysql-server
  yum  -y install memcached
  yum  -y install phpmyadmin
  service memcached restart
  /etc/init.d/mysqld restart
  /etc/init.d/httpd restart
  cp -R /usr/share/phpMyAdmin/ /var/www/html/
  #find deny from all and comment it in the entire file
  vim /etc/init.d/httpd/phpmyadmin.conf


#### 安装sendmail

    yum -y install sendmail

#### 安装EPEL软件包

   wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
   sudo rpm -ivh epel-release-6-8.noarch.rpm

#### 安装reviewboard

    yum -y install ReviewBoard

#### 数据库

  mysql -uroot -p123456;
  create database reviewboard default charset utf8 collate utf8_general_ci;

#### 创建站点
  rb-site install /var/www/reviewboard
  #更改文件拥有者为apache（web服务器）（在site创建完成时，会提示做如下更改）
  chown -R apache /var/www/reviewboard/htdocs/media/uploaded
  chown -R apache /var/www/reviewboard/htdocs/media/ext/
  chown -R apache /var/www/reviewboard/data/
  #将reviewboard的配置文件拷贝到apache配置文件下
  # cp /var/www/reviewboard/conf/apache-wsgi.conf /etc/httpd/conf.d


#### 重启apache

  /etc/init.d/httpd restart

#### reviewboard使用

  如果添加repo的时候出现错误permission denied accessing the local Git repository, 可能原因是git仓库地址的权限问题，改下权限就行，以便apache用户组也能访问


