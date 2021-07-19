# 原创

： 《python3网络爬虫开发实战》学习笔记：pyspider报错Exception: HTTP 599: SSL certificate problem...

# 《python3网络爬虫开发实战》学习笔记：pyspider报错Exception: HTTP 599: SSL certificate problem...

报错信息：Exception: HTTP 599: SSL certificate problem: unable to get local issuer certificate

之前刚进去的第一个页面时候也是这个报错，但是等到今天它就没有了，我准备再等等。万一好了了！！<br/>
之前第一个页面就是这个页面（出现报错）：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020032317340594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
现在是这个页面<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020032317344783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
报错信息一样，都是Exception: HTTP 599: SSL certificate problem: unable to get local issuer certificate。

之后找到了崔大神的《PySpider HTTP 599: SSL certificate
problem错误的解决方法》的第二步进行了pyspider0.4的更新，结果遇到pycurl无法下载。用ainivip的《Windows下安装pyspider时pycurl没有安装成功的解决方法》下载了一个pycurl-7.43.0.3-cp37-cp37m-win_amd64.whl，结果还是报一样的错。<br/>
最后想着即使pyspider0.3.10即使无法后续使用，但是可以对照0.4进行更新。然而在再一次进入的时候，忽然发现其实def index_page(self, response):<br/> for each in
response.doc(‘a[href^=“http”]’).items():<br/> self.crawl(each.attr.href, callback=self.detail_page)
也可以加一个defvalidate_cert=False。结果成功了。

[1]https://cuiqingcai.com/2703.html<br/> [2]
Windows下安装pyspider时pycurl没有安装成功的解决方法<br/> http://f.dataguru.cn/thread-942621-1-1.html<br/> (出处: 炼数成金)
