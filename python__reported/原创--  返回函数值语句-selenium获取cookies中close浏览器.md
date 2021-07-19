# 原创

： 返回函数值语句：selenium获取cookies中close浏览器

# 返回函数值语句：selenium获取cookies中close浏览器

我在通过selenium使用headless的Firefox获取需要访问网站的cookies时，发现返回函数值的return语句与关闭浏览器两者不可得兼。<br/>
因为如果需要函数返回cookies，那么浏览器关闭命令就需要在return后面，但是return不仅具有返回的作用还具有break的作用，如下图：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410092157668.png"/><br/>
导致浏览器无法关闭，如下图（在任务管理器中）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410092425951.png"/><br/>
浏览器无法关闭会导致占用大量内存，不利于电脑运行，直观感受就是会卡顿。

而将浏览器关闭命令提前，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410092828960.png"/><br/> 会报错：<br/> raise
exception_class(message, screen, stacktrace)<br/> selenium.common.exceptions.InvalidSessionIdException: Message: Tried
to run command without establishing a connection

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410092807120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
其实就是无法获取所需要东西，因为提前关闭了浏览器。<br/> 那么问题来了，有没有什么办法使得仅能够关闭浏览器有获得返回返回值呢？<br/>
我找了一下python的内置函数却没有发现，但是与return作用相似还有yield，yield可以返回函数值又不会中断后面的命令。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410093231482.png"/><br/>
如下图，任务管理器中没有了Firefox:<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200410093646106.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> **
然而**…<br/> 这里有个问题就是非常麻烦，因为yield返回的是list类型，需要进行字符串处理。

暂时没有找到其他方法，如果python存在return返回函数值又不中断后面命令的语句，或者有更加简单的方法，希望大神能够指教！！！！！
