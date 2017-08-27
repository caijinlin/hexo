---
title: php like查询json字符串的某一个字段
tags: []
date: 2015-04-20 08:00:00
---

### 查询json字段需要过滤特殊字符, 数据量大了之后可能存在性能问题

	比如donate_form_data存取 

	{
		"name":"\u79d1\u5fe0",
		"new_item_6":"\u7535\u5b50\u90ae\u7bb1",
		"title":"这是一段描述",
		"mobile":"",
		"gender":"\u7537",
		"new_item_1":"\u4e0d\u662f",
		"new_item_2":"",
		"new_item_3":"",
		"new_item_4":"",
		"new_item_5":"\u5426",
		"address_widget_province":"",
		"address":"",
		"browser_user_agent":"Mozilla\/5.0 (Linux; U; Android 5.1.1; en-us; HUAWEI P7-L00 Build\/HuaweiP7-L00) AppleWebKit\/533.1 (KHTML, like Gecko)Version\/4.0 MQQBrowser\/5.4 TBS\/025440 Mobile Safari\/533.1 MicroMessenger\/6.2.5.50_rbb77fd6.621 NetType\/WIFI Language\/en",
	}

	需要查询donate_form_data 中的title
 	$sql = "
        SELECT 
            sum(cd.donate_amount) donate_amount, count(cd.donate_amount) donate_count
        FROM 
            donates cd
        WHERE 
            and cd.donate_form_data like '%s'
        ";
    $query = '这是一段';
    $title = str_replace('\\', '_', json_encode($query));
    $donates[$item['id']] = M("")->query($sql, '%' . $title . '%');