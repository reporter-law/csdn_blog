# 原创

： 案例爬取（其二）:Error:11004、状态码200但是返回None——自己坑自己的步骤

# 案例爬取（其二）:Error:11004、状态码200但是返回None——自己坑自己的步骤

第二步：进行具体正文的提取，此时不止出现前面的代理问题：Error:10060,还时长出现Error:11004,和返回None

简直一脸懵逼，他妈的又全是英文，还不仅python错误，连window的各种错误都出来了！！！！！！！！！！！！！！！！！！！！

<img alt="" src="https://img-blog.csdnimg.cn/20200420104146207.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420100819795.png"/>

各种查找都没有找到解决方法！！！

各种尝试中发现当我一个一个输入url时，成功了！！！！<br/> 但是进行遍历提取时却是状态码200 和返回None!!!

难道要一个一个的自行传递url，一遍一遍的运行，绝对不可能！！！

真香！！一个一个的传递url,最终到第3个，实在受不了，于是开始再次检查。<br/> 多方查找，既然状态码200正常，那么就只能是后面的内容有问题了，结果没有发现。

没有办法的我就只能向前找，结果错误竟然在前面，200的状态码，错误竟然在前面！！！

奇怪的问题来了：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420105603787.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200420105656370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
两个url进行判断为不相等，一开始还以为是数据结构不一致，结果加了str()没有用，加上‘’也没有用。<br/> 最后查看txt文档时终于想起来，原来是在写入txt时为了好看，进行了换行，因而提取的url中也会存在换行符！！！

2020年4月28日：<br/>
对于个人需求的数据来说，有时觉得爬虫十分鸡肋，因为爬取数据就是希望使用大量数据，但是基本上都会碰到ip限制，但是购买ip就要花钱，相当于就是在买数据，为什么不省下学习时间来直接购买要的数据，价格相差也不大甚至更低，或许收获就是学了知识，但是知识本身就是够用就行并不完全是为了学习而学习。

2020年5月1日：<br/> 每次到第40000页后都是没有内容，其header为<br/> {‘Server’: ‘nginx/1.6.0’, ‘Date’: ‘Fri, 01 May 2020 02:02:56 GMT’,
‘Content-Length’: ‘0’, ‘Connection’: ‘close’, ‘Set-Cookie’: ‘JSESSIONID=A5EA74140CEDF8C271412C6D3BC21E30;
Domain=.fae.cn; Path=/; HttpOnly’, ‘Content-Language’: ‘en-GB’}

可见’Content-Length’: '0’即没有内容，可能是我爬取有问题？<br/> 但是网页中直接跳转尾页时也没有内容，或者网站宣传的100万份裁判文书是假的？？？？？？

尾页跳转内容：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501100958625.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
