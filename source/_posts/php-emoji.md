---
title: php处理emoji表情
tags: []
date: 2016-03-01 08:00:00
---

手机端网页输入表情时，显示的时候会乱码。而且android和iphone两种机型对emoji表情的解码不一样，导致一些不兼容问题。需要一种方案处理emoji表情，自己在做的时候，总结下三种方案。

#### 三种方案

	1.使用utf8mb4存储（但不完美）
	2.使用现有的php-emoji库
	3.composer require mojione/emojione

#### 方案一(utf8mb4)

    修改编码, utf8mb4兼容utf8，且比utf8能表示更多的字符。可以存储emoji表情字符

    修改如下：

    1.设置表编码和相应字段编码为utf8mb4
    2.设置连接数据库编码为utf8mb4

    ALTER TABLE `users` CHARACTER  SET utf8mb4 COLLATE utf8mb4_general_ci;
	ALTER TABLE `users` CHANGE `comment` `comment` TEXT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL;

	DB_CHARSET => 'utf8mb4'; //如果thinkphp，配置文件中修改连接数据库编码

	缺点: iphone手机上不能显示android手机发的表情
	优点:  简单，不用修改代码


#### 方案二 [(https://github.com/iamcal/php-emoji)](https://github.com/iamcal/php-emoji)

	使用php-emoji库处理，原理是: 手机发的表情字符存入到数据库中是一段html, 显示的时候通过引用emoji库的css， 显示表情。

	修改如下:

	1.引入emoji.css, 并确保emoji.png引入到css中指定的位置

	2.引入emoji.php, post过来的内容作如下处理：

	$content = emoji_docomo_to_unified($content);
	$html = emoji_unified_to_html($content);

	//将$html存入数据库，$html类似<span class="emoji emoji1f609"></span>

	缺点: 通过css实现，需要加载emoji.css和emoji.png和emoji.php, 依赖外部
	优点: 兼容性好，web, android, iphone都可查看表情

#### 方案三 [(https://packagist.org/packages/emojione/emojione)](https://packagist.org/packages/emojione/emojione)

	通过composer引入: `composer require mojione/emojione`

	保存时: Emojione::toShort($comment));

	显示时: Emojione::shortnameToUnicode($comment);

	缺点：第三方输入法（比如百度输入法）的表情不是完全支持
	优点：目前为止兼容性最好的

