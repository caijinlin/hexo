---
title: hexo常用命令
date: 2015-03-07 08:02:28
tags:
---

## Quick Start

### 标签

``` bash
[tag1, tag2, tag3]
```

### 分类

```bash
category1
```

### 新增页面
```bash
hexo new page 'about'
```
接着把链接加上，themes/yourthemeName/_config.yml里面的menu一项，添加一行About: /about。


### 新增rss

```bash
npm install hexo-generator-feed --save
hexo clean
hexo server
```

### 从xss迁移文章

获取原博客的文章rss，放在博客根目录下，通过hexo-migrator-rss导入进来，十分高效，时间自动转化了。

```bash
npm install hexo-migrator-rss --save
hexo migrate rss old.xml
```

如图：

![](http://7xirhj.com1.z0.glb.clouddn.com/blog/assert/images/hexo-migrate-xml.jpg)