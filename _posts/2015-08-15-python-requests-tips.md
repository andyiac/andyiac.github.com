---
layout: post
category: ideology
tags : [python]
title : python 开源项目 requests 抓取中文网页乱码
---
{% include JB/setup %}


最近在写一个Android客户端，没有数据就拿python抓了一个网站[githubrank.com](http://githubrank.com)来测试，
用到了开源项目[requests](https://github.com/kennethreitz/requests) 

抓取数据代码如下：


	import requests

	# crawler ranking

	r = requests.get("http://githubrank.com")

	print r.text


数据拿到后打印了下发现中文是十六进制,如下：


	 \xe4\xba\x91\xe9\xa3\x8e


使用utf-8能正确解码：


	 print '\xe4\xba\x91\xe9\xa3\x8e'.decode('utf-8')

	 风云


查看响应编码发现：


	r.encoding

	'ISO-8859-1'


是'ISO-8859-1'编码

google了一番发现requests只会简单的从服务器响应头的Context-Type 去获取编码，如果有Charset才能正确尸蟞编码，否则使用默认的ISO-8859-1

解决办法即使用ISO-8895-1 encode一下，在使用正确的charset去descode,不过可能再转换过程中引起数据丢失。


	print r.text.encode('ISO-8859-1').decode('utf-8')


正常显示

[refer](http://www.zhetenga.com/view/python的requests类抓取中文页面出现乱码-0abbaa140.html)

