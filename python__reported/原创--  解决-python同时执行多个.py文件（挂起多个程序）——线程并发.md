# 原创

： 解决：python同时执行多个.py文件（挂起多个程序）——线程并发

# 解决：python同时执行多个.py文件（挂起多个程序）——线程并发

python IDE :pycharm<br/> 运行任务：代理池（Python爬虫代理IP池(proxy pool)），url：https://github.com/jhao104/proxy_pool

代理池启动方式：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200411092716981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

如上所述：启动代理池时发现需要同时启动两个py文件，但是每次去找到两个不再同一个位置的文件然后启动它们特别麻烦。<br/> 于是，我想在一个py文件中进行代理池调用的集成。

在启动这个代理池时遇到了麻烦，每当我启动这个代理池时，需要运行两个命令<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041109321926.png"/><br/>
但是在运行过程中运行到第一个命令后，第二个命令不会允许，因为前一个命令是一个不会自动终止的爬取ip地址的程序，不关闭时会一直挂着，于是第二个命令就无法运行。

解决方法一：在Allow running in parallel选项打勾（****无效**！！！**）<br/> 博主nihate：《pycharm中同时运行多个.py文件》的解决方法为在pycahrm run 的 edit config
里面勾选一个Allow running in parallel选项。<br/>
但是这个是让同一个py文件运行多次，并不符合其标题名同时运行多个.py文件。因为同时运行多个.py文件应当为同时运行多个不同的.py文件，如果同时运行多个相同.py文件应该叫多次运行一个.py文件。其检测效果为：一个py文件可以同时运行，如下图：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200411094058740.png"/>

有的文章认为在命令中增加 “&amp;”,以及自己尝试的“and”这样都只能运行第一个py文件,实测均为无效<br/> 解决方法二（***最终解决方法！！！！***）：

线程并发<br/> 博主weixin_30684743：《python一个文件里面多个函数同时执行(多进程的方法，并发)
》解决了我的这个问题<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200411094850412.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
运行结果如下图：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200411095237224.png"/><br/>
黑色部分为第一个爬取ip并验证的py文件的运行结果，第二个为启动api以备ip地址调用的py文件。

[1]https://blog.csdn.net/nihate/article/details/85164458?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158657004819724845034038%2522%252C%2522scm%2522%253A%252220140713.130102334…%2522%257D&amp;request_id=158657004819724845034038&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task-blog-soetl_SOETLBAIDU-3<br/> [2]https://blog.csdn.net/Eric_LH/article/details/86482326?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158657004819724845034038%2522%252C%2522scm%2522%253A%252220140713.130102334…%2522%257D&amp;request_id=158657004819724845034038&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task-blog-soetl_SOETLBAIDU-2<br/> [3]https://blog.csdn.net/weixin_30684743/article/details/101355138?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158656961919724811810701%2522%252C%2522scm%2522%253A%252220140713.130056874…%2522%257D&amp;request_id=158656961919724811810701&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task-blog-blog_SOOPENSEARCH-1
