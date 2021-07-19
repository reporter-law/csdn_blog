# 原创

： IP访问限制:API获取IP效用最大化

# IP访问限制:API获取IP效用最大化

在访问某网站时，网站具有访问次数限制，大概是10次左右。10次后就会出现访问次数过多受限，请拨打xxxxxxxx谢谢支持！<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423145316261.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
报错：<br/> 在requests.exceptions.ConnectionError会导致返回[WinError 10060]
由于连接方在一段时间后没有正确答复或连接的主机没有反应，连接尝试失败。或者ConnectionResetError: [WinError 10054] 远程主机强迫关闭了一个现有的连接。<br/>
我爬取的这个网站导致的这种访问限制的原因在于ip问题<br/> 解决方法：需要换IP<br/>
换ip，如果用免费的proxy_pool，其实有时可以，但是对于特定网站，需要进行特定网站的再次筛选，因为一般proxy_pool会以百度等网站作为验证ip可行性的测试网站，然而这并不意味着可以作为自己试图爬取的网站的ip，因为需要自己进行测试。

```
 def check_proxy():
	index = 1
	try:
    	while True:
        	proxy = get_proxy()
        	url = xxx
        	r = requests.get(url, proxies=proxy)
        	if r.status_code == 200:
            	print('返回可用代理，以下为抓取的url.....................................................................')
            	return proxy
       	 	else:
            	print('这是第%d个代理测试' % index)
            	index += 1
            	continue
	except requests.exceptions.ConnectionError as c:
    	print(c)
    	time.sleep(10)

```

我要爬取的网站在可用的ip中大致只有5个左右，太少了。<br/> 于是需要购买ip<br/>
ip软件其实较好，因为会自动换ip，但是我用的那款有点不好的地方在于没2小时就会自动掉线，买了一天，本准备用一夜全部爬完，但是中途掉线，￥￥￥都没了，于是放弃。<br/> 于是注册试用成了我的常态<br/>
除了ip软件还遇到了获取API的这种卖法

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423152120637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
防止广告嫌疑，尽量选择没有这种API获取IP方式网页的名字！！！

某个卖代理的网站注册免费送了1000个，但是问题是不会用这种有时效限制又需要获取的，于是左右捣鼓，明白了这种其实和请求网页是一样的，requests
url，就会返回ip，但是需要对ip进行字符串处理，形成代理的字典格式（代理必须字典格式！！！！！！）

重点来了！！！！！！！！！！！！！！<br/> 然而另一个问题来了，每次请求url返回一个ip，但是每次ip时长几分钟，一个一个提取十分费力。<br/>
有没有办法自动完成，就我爬取的网页而言，这需要让函数调用十次返回同样的值，而第十一次调用返回另一个IP，类似于数学中的分段函数。<br/>
尝试过许多方法，比如先写入txt文件，然后隔一段时间进行自动删除，然后更新，但是这种想法没有办法用python完成，总是出现各种问题。<br/>
本来希望客服设置url每分钟返回同一个IP，但是不行：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423153405980.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423153438867.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423153500592.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

终于想到了另一个方法（其实非常简单）：<br/> 前提：知道访问次数限制，<br/> 我之前知道范围次数限制大致10次左右，于是对提取到的IP进行复制，复制十次，然后返回，这样每个调用函数时对调用函数值进行十次利用即可。<br/>
让IP效用最大化，既在时效内用了IP又让IP达到被封次数

```
def get_web():
	url = 'http://http.tiqu.alicdns.com/getip3?num=1&amp;type=1&amp;pro=&amp;city=0&amp;yys=0&amp;port=1&amp;pack=94267&amp;ts=0&amp;ys=0&amp;cs=0&amp;lb=1&amp;sb=0&amp;pb=4&amp;mr=1&amp;regions=&amp;gm=4'
	try:
    	r = requests.get(url)
    	if r.status_code == 200:
        	proxies = {
           	 'http': 'http://'+ r.text.strip(),
           	 'https': 'https://' +r.text.strip()
       			 }
       		 '''proxies必须是字典类型——-—— 
            	否则报错：no_proxy = proxies.get('no_proxy') if proxies is not None 	else None
            	AttributeError: 'set' object has no attribute 'get' '''
        	proxies_ = proxies
        	proxies_1 = proxies
        	proxies_2 = proxies
        	proxies_3 = proxies
        	proxies_4 = proxies
        	proxies_5 = proxies
        	proxies_6 = proxies
        	proxies_7 = proxies
        	proxies_8 = proxies
        	proxies_9 = proxies
        	proxy_pool = [proxies,proxies_,proxies_1,proxies_2,proxies_3,proxies_4,proxies_5,proxies_6,proxies_7,proxies_8,proxies_9]
        	return proxy_pool
	except ConnectionError:
    	return None

```

现在使用“ok”<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200423154038486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
