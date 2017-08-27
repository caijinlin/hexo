---
title: 搭建git服务器
tags: []
date: 2015-02-11 08:00:00
---


### centos搭建git服务器

一些公司或者某些项目不适合放入github中，希望能有一个完全私有的仓库，如果有一台服务器，可以搭建git服务器，专门用于git服务。

#### centos搭建git服务器


step1. 安装git(如果没有就安装)


    yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
    yum install git


step2.创建一个git用户，用来运行git服务


    groupadd git
    adduser git -g git
    passwd git  /**设定密码*/


step3.密钥管理

    收集所有需要登录的用户的公钥，公钥位于id_rsa.pub文件中，把我们的公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
    cd /home/git/
    mkdir .ssh
    chmod 700 .ssh
    touch .ssh/authorized_keys
    chmod 600 .ssh/authorized_keys

step4.初始化git仓库

    cd /srv
    mkdir learngit.git
    chown git:git learngit.git
    git init --bare learngit.git

step5.客户端clone仓库

    git clone git@192.168.45.4:/srv/learngit.git

step6. 客户端push操作

    cd learngit
    touch readme.txt
    git add .
    git commit -m 'init'
    git push origin master

【Notice】由于远程git服务器远程仓库里只是一个代码库，所以push代码到git服务器上，也看不到刚push过来的内容，这是正常的，可以进行pull等操作。