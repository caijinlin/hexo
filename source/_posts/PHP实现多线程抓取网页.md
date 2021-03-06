---
title: PHP实现多线程抓取网页
tags: []
date: 2014-06-23 08:00:00
---

### PHP实现多线程抓取网页

使用PHP的cURL库可以简单和有效地去抓网页。你只需要运行一个脚本，然后分析一下你所抓取的网页，然后就可以以程序的方式得到你想要的数据了。无论是你想从从一个链接上取部分数据，或是取一个XML文件并把其导入数据库，那怕就是简单的获取网页内容，cURL 是一个功能强大的PHP库。本文主要讲述如果使用这个PHP库抓取网页。

<!-- more -->            

#### 开启curl库

首先要确定我们的PHP是否开启了这个库，如果你是在Windows平台下，需要改一改你的php.ini文件的设置，找到php_curl.dll，取消前面的分号就行：

    extension=php_curl.dll

##### 利用curl抓取网页代码

    <?php
    $urls = array(    
        'http://www.baidu.com/',
        'http://www.caijinlin.com/',
        'http://caijinlin.github.io'
    );   
    $save_to='./res.txt';   // 把抓取的代码写入该文件       
    $st = fopen($save_to,"a");      
    $mh = curl_multi_init(); //创建多个curl句柄
    foreach ($urls as $i => $url) 
    {   
    $conn[$i] = curl_init($url);   //创建一个curl句柄
    curl_setopt($conn[$i], CURLOPT_USERAGENT, "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)");   
    curl_setopt($conn[$i], CURLOPT_HEADER ,0);  // 这里不要header，加块效率
    curl_setopt($conn[$i], CURLOPT_CONNECTTIMEOUT,60);   //设置超时时间
    curl_setopt($conn[$i],CURLOPT_RETURNTRANSFER,true);  // 设置不将爬取代码写到浏览器，而是转化为字符串  
    curl_multi_add_handle ($mh,$conn[$i]);   //向curl批处理会话中添加单独的curl句柄
    }   
    do 
    {   
        curl_multi_exec($mh,$active);//循环执行   
    } while ($active);   
    foreach ($urls as $i => $url) 
    {   
        $data = curl_multi_getcontent($conn[$i]); // 获得爬取的代码字符串   
        fwrite($st,$data);  // 将字符串写入文件。当然，也可以不写入文件，比如存入数据库   
    } // 获得数据变量，并写入文件   
    foreach ($urls as $i => $url) 
    {   
      curl_multi_remove_handle($mh,$conn[$i]); // 移除curl批处理句柄资源中的某个句柄资源  
      curl_close($conn[$i]);   
    }    
    curl_multi_close($mh); //关闭多个cURL 多个句柄
    fclose($st);  //关闭文件
    ?>

#### 效果预览

抓取3个网页，通过curl可以达到多线程，进行同时抓取，而不必等到第一个网页抓取完毕，再抓取第二个。
res.txt文件中，存放了3个网页的代码，分别复制出来，存放在html文件中，就可以看到他们的效果如下。

百度页面

![邻接表](/assets/images/baidu.png)

我的基于jekyllbootstrap的博客

![邻接表](/assets/images/jekyllblog.png)

我的wordpress博客

![邻接表](/assets/images/wordpress.png)