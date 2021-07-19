# 原创

： 《python3网络爬虫开发实战》13.8笔记——记自己学习的困惑

# 《python3网络爬虫开发实战》13.8笔记——记自己学习的困惑

《python3网络爬虫开发实战》13.8为scrapy对接selenium

复制书中的源码无法爬取；由于淘宝需要会员登录后才能使用，不想麻烦的登录。<br/>
爬取页面<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328143815977.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
失败原因：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328143942998.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
因而选取的爬取对象是知乎：<br/> 问题一：phantomjs在界面会存在警告"UserWarning: Selenium support for PhantomJS has been deprecated, please use
headless versions of Chrome or Firefox instead"，因为selenium新版本不在支持phantomjs;<br/> 解决方法：降版本安装或者换成Chrome or
Firefox的无界面；selenium需要降至selenium2.48.0。参见博主本是少年的《Selenium support for PhantomJS has been deprecated解决方案》

问题二：由于xpath可以在浏览器中复制，比较懒的我就使用了xpath选择器，如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328145013591.png"/><br/>
这里的问题在于如果在/div的前面没有一点即./div的话就会导致。xpath跨越遍历的topic进入topics里面寻找节点，这个问题整整困扰了我一天，虽然崔大神的书中确实介绍了这个，但是我在例子中练习的时候返回空值，毕竟是18年的还以为有什么问题就没有在意这一点，结果在这里卡住了整整一天。

问题三：使用phantonjs会存在无法下翻（知乎下滑出现新内容），界面似乎不加载js,和在ternimal中点击url打开的explore一样，只有前面几个，无法下滑；因而使用chrome较好。但是chrome的无界面浏览参数存在变化。<br/>
网上的scrapy+selenium+chrome的技术路线中用chrome传参为options
但是这个参数会报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328151303371.png"/><br/>
原因为这个参数已经改变了，变成chrome_options,如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328151430147.png"/>

出现下图基本成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200328152613122.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

[1]https://blog.csdn.net/qq_43055565/article/details/99345542?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158537770419725256732602%2522%252C%2522scm%2522%253A%252220140713.130056874…%2522%257D&amp;request_id=158537770419725256732602&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task
