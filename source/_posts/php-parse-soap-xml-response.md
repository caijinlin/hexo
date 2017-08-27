---
title: php parse soap xml response
tags: []
date: 2017-03-01 08:00:00
---

#### 最近公司的一个需求，和外部对接需要用到xml。
说明：XML本身不算复杂，但是，加上DTD、XSD、XPath、XSLT等一大堆复杂的规范以后，任何正常的软件开发人员碰到XML都会感觉头大了，最后大家发现，即使你努力钻研几个月，也未必搞得清楚XML的规范。> 使用场景：请求外部webservie，对方以xml的形式的返回，我们需要拿到数据，看起来很简单，但不懂xml与xsd就有点麻烦了。

#### 遇到问题 =&gt; 发现问题
通过传统解析xmlToJson, xmlToArray，怎么样也获取不到数据分析返回的xml，发现是xsd，并且含有命名空间The problem here is that your attribute has a namespace, so you need to register the ns with SimpleXML XPath and use it in your XPath query.

#### 解决方法
http://stackoverflow.com/questions/26511858/parsing-soap-xml-response-with-php/26512336#26512336<div class="language-xml highlighter-rouge">

	<?xml version="1.0" encoding="utf-8"?>
	<DATARESULT xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://tempuri.org/">
	  <TABLE>
	    <diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">
	      <DocumentElement xmlns="">
	        <DATA diffgr:id="TABLE1" msdata:rowOrder="0" diffgr:hasChanges="inserted">
	          <FIED1>1221</FIED1>
	          <FIED2>2332</FIED1>
	        </DATA>     
	        <DATA diffgr:id="TABLE2" msdata:rowOrder="0" diffgr:hasChanges="inserted">
	          <FIED1>1221</FIED1>
	          <FIED2>2332</FIED1>
	        </DATA>    
	      </DocumentElement>
	    </diffgr:diffgram>
	  </TABLE>
	  <ResultMsg />
	</DATARESULT>

注册命名空间，匹配相应节点，取出数据

	// request webservice for get data
	$client = new SoapClient($url, $params);
	$result = $client->getData();

	// parse data
	$xml = simplexml_load_string($result->responseXml);
	$xml->registerXPathNamespace('d', 'urn:schemas-microsoft-com:xml-diffgram-v1');
	$results = $xml->xpath('//Table');
