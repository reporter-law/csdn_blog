# 原创

： 《python3网络爬虫开发实战》学习笔记：pyspider all报错的解决

# 《python3网络爬虫开发实战》学习笔记：pyspider all报错的解决

'http_au@[TOC](pyspider all 报错解决)

pyspider all 出现报错，一共三个报错。<br/> 之前有两个报错，csdn上的大神已经解决了。参见《pyspider all运行出错：①SyntaxError: invalid syntax，② - Deprecated
option ‘domaincontroller’: use 'http_au》。前面这两个图也是来源此作者

第一个报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322175353199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
主要是async是python3.7的保留字，pyspider库中的有些文件与之重复而出现报错，就三个文件，这三个文件的找法可以参照《windows客户端pip安装pyspider完全指南（SyntaxError:invalid syntax、async语法报错、非引用替换关键字、全局查找针对性替换、Pycharm）》，async的具体位置在pycharm中会有红色标注，替换的词可以任意选择，我就在后面加了一个下划线即“async_”；

```

第二个报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322172457428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

这是由于WsgiDAV发布了新版本 pre-release 3.x，所以只要把版本降下来就好了。将wsgidav替换为2.4.1，在命令行下运行<br/> python -m pip install wsgidav==2.4.1。

第三个报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322172746826.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
如报错所说是import错误。werkzeug.wsgi中没有class DispatcherMiddleware。这个class DispatcherMiddleware在werkzeug\middleware中，path显示C:
\Users\Administrator\AppData\Local\Programs\Python\Python37\Lib\site-packages\werkzeug\middleware\dispatcher.py。<br/>
然后在app.py中64行输入“from werkzeug.middleware.dispatcher import DispatcherMiddleware” 即可
如下图<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322173749752.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
之后，输入pyspider all
就好了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322173938157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
正常运行如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200322174018169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> [1]: https://blog.csdn.net/u012424313/article/details/89511520?depth_1-utm_source=distribute.pc_relevant.none-task&amp;utm_source=distribute.pc_relevant.none-task<br/> [2]: https://blog.csdn.net/qq_40916793/article/details/100163293?depth_1-utm_source=distribute.pc_relevant.none-task&amp;utm_source=distribute.pc_relevant.none-task
