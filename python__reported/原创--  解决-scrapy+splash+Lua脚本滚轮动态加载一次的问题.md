# 原创

： 解决：scrapy+splash+Lua脚本滚轮动态加载一次的问题

# 解决：scrapy+splash+Lua脚本滚轮动态加载一次的问题

作为小白，对于滚轮动态加载没有想到简便的解决方法，主要是通过for循环。<br/>
在学习之前的scrapy+selenium爬取的就是知乎页面，知乎页面是滚轮动态加载的，使用滚动到底这个js命令时发现只能翻转一页<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200329105325748.png"/><br/>
于是在’window.scrollTo(0,document.body.scrollHeight)'
之前增加了一个for循环后可以成功加载多次。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200329105621748.png"/>

在scrapy+splash+Lua脚本滚轮动态加载中也是如此，只是使用lua脚本的for循环<br/>
lua脚本的for循环实例：<br/> <img alt="这个实例可以参见脚本之家的脚本专栏 → Lua → Lua中的for循环" src="https://img-blog.csdnimg.cn/20200329105819166.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
在scrapy中传入为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200329105941195.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
传入后cmd的运行：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200329110040802.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
mongo数据库中的爬取的数量明显增加<br/> <img alt="" src="https://img-blog.csdnimg.cn/20200329110324247.png"/><br/> 之前的爬取数量为27

但是这里存在的问题是：不知道能否加载完，其次for循环过多会影响速度；如果要比较精确的加载完且不浪费循环需要进行计算，这是个很麻烦的事情。

[1]https://www.jb51.net/article/66867.htm
