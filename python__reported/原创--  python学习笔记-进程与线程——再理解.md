# 原创

： python学习笔记：进程与线程——再理解

# python学习笔记：进程与线程——再理解

在上一篇《图解：进程与线程——实用主义理解》中我以为进程与线程创建好了就可以自动分成多个进程与线程，即一个函数被自动分成几个进程或者线程然后执行。

但是，后来发现似乎并不是这样的。在简单函数试验时发现速度确实提高了，可以参见之前的这篇文章《图解：进程与线程——实用主义理解》，但是我在一个爬虫项目试图运用多线程时发现与我没有用多线程时似乎速度没有快多少。——这是在提取一个网页中的跳转的url<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408135630548.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408135712103.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408135734783.png"/>

但是如上图所示，虽然每页的url提取非常快，但是仍然是一页一页的按序提取的，我需要提取的url一共一百万个，每页12个链接，需要提取10万个网页需要花费很长的时间。<br/> 于是我想是不是我哪里理解错了。<br/>
之后看到一篇博文《Python学习笔记 concurrent.futures 模块》探讨另一个多线程包 ——"
concurrent”<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408140152881.png"/><br/>
这里突然出现了线程池：<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408140843429.png"/><br/>
又是多方寻找测试才明白一个submit<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408141400898.png"/><br/>
或者Thread<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408141431114.png"/>

只是一个线程，多个线程需要自己提交多个函数或者一个函数进行执行环节的拆分（对于上面这个爬虫项目就要拆分页数）；创建多个Thread对象<br/>
按照拆分页数进行拆分后提交多次后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020040814321080.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408141848366.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
或许划分为五个还是太慢了,但是电脑内存上升的也很快！！！！！
