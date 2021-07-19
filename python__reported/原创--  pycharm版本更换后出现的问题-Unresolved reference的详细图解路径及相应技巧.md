# 原创

： pycharm版本更换后出现的问题：Unresolved reference的详细图解路径及相应技巧

# pycharm版本更换后出现的问题：Unresolved reference的详细图解路径及相应技巧

pycharm版本更换：<br/> 由于pycharm2019.3.4启动缓慢，换成了pycharm2018.3.7,再次启动这个项目出现报错。<br/> 项目：<br/>
使用jhao代理池，需要同时启动ProxyScheduler.py和ProxyApi.py两个文件。<br/> 出现报错：<br/> 找不到模块（ModuleNotFoundError: No module named
‘Schedule’）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419102726774.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是直接运行可以：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419102812419.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
进入ProxyScheduler.py文件内部发现import处出现标红：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419102924654.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
报错内容为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419103005454.png"/><br/>
其实就是找不到调度的文件，但是调度方法没有错误。<br/> 解决方法测试；<br/>
1、更改解释器，换成项目下的解释器而不是原来的c盘下的解释器<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202004191031311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419103356745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
无效，反而导致pip安装的包都出现这个错误

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041910342326.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419103436419.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
解决方法二：<br/> 参见《[Editor]PyCharm中出现怪异的Unresolved Reference…》，url:https://www.jianshu.com/p/9555310f1920<br/>
问题是没有“你要做的就是：File → Settings → Editor → File Types → Ignore files and folders，干掉框框中的：**init**.py;，”这个选项<br/>
现为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419103720787.png"/>

解决方法三：source标记<br/> 《Inspection info: This inspection detects names that should resolve but don’t. Due to dynamic
dispatc》，url:https://blog.csdn.net/sinat_40292249/article/details/90760683<br/>
如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419103930255.png"/><br/>
但是一样的：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041910400342.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

解决方法四：<br/>
基于解决方法三的详尽，source标在初始的文件夹似乎无效，有效的需要标记在更细小的文件夹，即<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104241879.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104301322.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104326900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

二、清除不想看见的文件夹<br/> 基于解决方法二的延伸，既然__init__.py被忽略可以重新找到，那么这个不想看见的.idea也可以这样干，添加这个文件夹

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104717954.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104637721.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419104806241.png"/>

三、配置快捷键运行py文件时总是出现小方框

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419105154306.png"/><br/> 原因快捷键配置错误<br/> 运行与run不是一回事<br/>
前者是运行，后者是run<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419105313134.png"/><br/>
解决方法：重新配置快捷键<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419105401278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419105425203.png"/>

设置这个运行虽然可以运行py文件，但是运行的是前一个文件而不是限制选中的文件<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041911023274.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
正确的配置为运行上下文配置<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419110331335.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200419110405117.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
部分内容参见简书作者：maxzhao_《IDEA使用技巧》<br/> 【1】https://www.jianshu.com/p/9555310f1920<br/>
【2】https://blog.csdn.net/sinat_40292249/article/details/90760683<br/> 【3】https://www.jianshu.com/p/90ed3d890f61
