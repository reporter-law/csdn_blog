# 原创

： Selenium+Firefox的自动下载（去掉下载弹窗）

# Selenium+Firefox的自动下载（去掉下载弹窗）

### Selenium+Firefox的自动下载（去掉下载弹窗）

# 一、去掉下载弹窗的优点

检索键盘鼠标自动化控制模块的导入<br/> 可以无头化运行，不影响同时进行的其他的任务

# 二、去掉下载弹窗的一般命令

```
from selenium.webdriver import FirefoxProfile
#导入相应的设置模块
profile = webdriver.FirefoxProfile()
#实例化
profile.set_preference('browser.download.dir', path.strip('\u202a'))
#设置下载路径
profile.set_preference('browser.download.folderList', 2)
#设置下载存储方式，2为自定义路径、设置成 0 表示下载到桌面；设置成 1 表示下载到默认路径
profile.set_preference('browser.download.manager.showWhenStarting', False)
#在开始下载时是否显示下载管理器
profile.set_preference('browser.helperApps.neverAsk.saveToDisk', 'application/zip,application/octet-stream')
#对所给出文件类型不再弹出框进行询问

```

此处命令参见Time-Traveler：《Selenium下载路径》，链接: [Selenium下载路径](https://blog.csdn.net/ALakers/article/details/107089895?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=selenium%20firefox%E4%B8%8B%E8%BD%BD%E6%97%A0%E5%BC%B9%E7%AA%97&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-107089895)
.

# 三、重点

上面命令说明比较简单，本人按照上述命令设置，在给定的例子中有效，但是我进行的是裁判文书的下载，结果始终无法自动下载，相关内容参见《中国裁判文书下载：selenium路线》，链接: [中国裁判文书下载：selenium路线](https://blog.csdn.net/python__reported/article/details/106575376)
.

兜兜转转找了好久这个问题一直没有解决，虽然也能用，但是始终不圆满

今天我用重新学习了一下，仔细看看了相关命令，某篇博文上看到关于firefox的新窗口变成新标签页的设置中，发现相关命令在<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200707222750522.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

相应的设置也只是在对参数进行设置，继续深入发现其实这些一般命令涉及到了firefox的设定，继续找到义甬君：《Selenium自动化下载文件Firefox配置教程&gt;》，链接: [link](https://blog.csdn.net/ywyxb/article/details/65628329?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase)
.

```
 profile.set_preference('browser.helperApps.neverAsk.saveToDisk', 'application/zip')

```

这个命令十分重要，但是应该没有问题啊！因为下载的就是压缩包，应该就是application/zip<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200707223110380.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

显示的也是zip的格式

但是后来去network中调试发现并非如此，下载弹窗的链接为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200707223232907.png"/><br/>
进去发现其content-Type并不是application/zip，而是,application/octet-stream，至此真相大白，解决了不能自动下载的问题<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200707223309728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
