---
title: 迁移jekyll到hexo
date: 2017-03-07 08:02:28
tags: [hexo, jekyll]
categories: 技术
---

### 一个美好的开始

原先的博客是通过jekyll生成的，现迁移到到hexo，通过原博客的xss文件完成文章的迁移

### 从xss迁移文章

获取原博客的文章rss，放在博客根目录下，通过hexo-migrator-rss导入进来，十分高效，时间自动转化了。

```bash
npm install hexo-migrator-rss --save
hexo migrate rss old.xml
```

### 迁移过程

![](http://7xirhj.com1.z0.glb.clouddn.com/blog/assert/images/hexo-migrate-xml.jpg)