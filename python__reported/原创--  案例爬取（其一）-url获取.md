# 原创

： 案例爬取（其一）：url获取

# 案例爬取（其一）：url获取

一、背景：<br/> 裁判文书爬取网站:中国裁判文书网、无讼网、聚法案例、法律家<br/> 中国裁判文书网：http://wenshu.court.gov.cn/<br/>
无讼网：https://www.itslaw.com/home<br/> 聚法案例：https://www.jufaanli.com/<br/> 法律家：http://www.fae.cn/<br/>
第一个反爬措施比较高级，暂时无法解决<br/> 第二个、第三个需要登录，登录后一天大概可以下载1000份左右的文书，如果需要下载更多就要会员或者更换账号，更换账号需要手机号<br/>
最后一个法律家最好爬，基本上属于静态网页，当然也有javascripts,但是不影响主体内容的爬取，用requests-lxml(bs4)等就可以了。<br/>
法律家裁判文书的爬取过程中，由于具体网页即裁判文书正文页访问存在访问次数限制，而非具体网页即裁判文书目录页的访问限制更低一些。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420101251916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420101308380.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

二、思路：<br/>
此处的爬取思路就是利用这两者的限制程度的不同分阶段进行，防止互相错误的干扰，先爬取url，然后爬取具体正文。（后来发现其实不用这么费劲，因为url的格式相同，完全可以自行构造一个一个的试）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020042010211764.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
在第一步就打转了半个月（主要是由于一些小问题、和比较穷的一个一个注册代理然后试用）<br/> 这里面的许多小问题在之前的文章中有所体现，尝试过许多方法，主要是：error10060,许多方法都是所谓的connection：close
;或者retry，但是其实不是的，而是代理的问题，关不关闭对这个爬虫没有什么问题。最后都是代理解决；<br/>
多线程或者多进程问题：开一两个线程速度太慢，爬了一天一夜才20000多的url,总共100万url就会爬死去，于是开多线程，一次开了40个线程，想着4个小时结束战斗；但是在20000次访问下没有问题的网站现在出现了问题，不是代理失效而是直接维护网站，对此我毫无办法。<br/>
代理问题：只想白嫖用免费的代理池，一个一个找代理池（github上的基本都找过了，有的我运行不起来特麻烦），找到比较好的崔庆才大神的代理池和jhao的代理池，但是代理错误太多，可用率太低；<br/>
然后一个一个代理软件注册试用，结果手机号不够用，于是试图使用免费手机号，但是无法注册。<br/> 使用免费短信、验证码平台即可，但是免费的手机号很大概率都被注册过了。

最后，发现其实url可以构造出来，怪我没有细看！！！！！<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420103445528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
仔细看url，发现其中<br/> http://www.fae.cn//cp/detail…html都是一样的，只有数字不一样，因而可以对数字进行构造，对不对没有关系，一个一个试过去，保障可以爬全。
