---
title: 使用SVN部署网站到新浪SAE
tags: []
date: 2014-06-24 08:00:00
---

### 使用SVN部署代码到SAE平台

最近3天在新浪SAE平台上部署了一个网站应用http://susecst.sinaapp.com/ ，本文主要写上传到SAE上面所遇到的问题。本地调试好代码后，通过svn上传http://sae.sina.com.cn/doc/tutorial/code-deploy.html#svn 

#### 数据库连接语句配置

    数据库服务器:w.rdc.sae.sina.com.cn:3307(在phpyadmin管理界面可见)
    数据库用户:应用首页的Access Key（点击显示可见）
    数据库密码:应用首页的Secret Key(点击显示可见)
    数据库名字:一般为app_应用名(数据库.sql文件需导入phpmyadmin)

#### 上传至新浪SAE后，发现文件乱码

避免文件乱码，首先要确定以下四种编码一致,假设为utf8

    数据库中表的结构编码utf8_general_ci
    文件编码<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    数据库执行语句编码 mysql_query(“set names utf8”);

有的时候得确认下文件编码:通过编辑器控制文件的标题编码，或者将文件另存为你需要的文件编码utf8。

#### 测试功能时，发现登录界面提交后显示

    Cannot send session cache limiter-headers aleady sent

![跳转错误](/assets/images/session.png)

搜索一番，发现基本是使用header跳转之前，不能出现任何echo语句，但是本地打开发现没有任何错误。最后在sae的代码管理器打开，发现了该文件前面有个小红点，删掉就行了，然后本地update，保持同服务器端版本一致

![文件前面小红点](/assets/images/sae.png)

