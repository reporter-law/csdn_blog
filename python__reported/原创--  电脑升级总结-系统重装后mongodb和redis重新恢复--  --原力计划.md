# 原创

： 电脑升级总结:系统重装后mongodb和redis重新恢复 ：

原力计划

# 电脑升级总结:系统重装后mongodb和redis重新恢复

### 系统重装后mongodb和redis重新恢复

# 缘由：

之前mongodb、 redis安装在win7环境下，但是win7对于docker需要下载docker tools非常麻烦、对于pycharm2020也不支持，加上电脑本身卡慢等等，使得我产生了对电脑进行升级的想法，并将之实现。
原本不想更好系统，用win7挺好的，准备迁移至固态硬盘。但是win7不再更新，许多程序会不再支持win7环境，想着晚换系统不如早换，不如还有一堆麻烦事，所以决定更新。<br/>
首先更换硬件，可以参阅《万字超详细图文教程：联想G510加装内存条、固态，机械移至光驱位》、《加装固态重装系统遇到开机慢：出现pxe2.0界面》；<br/>
其次是更换系统：《windows10系统精简：NTlite工具》、山外的鸭子哥的《Windows 10 LTSC 2019
正式版轻松激活教程》—链接: [link](https://www.landiannews.com/archives/51131.html/).<br/> 再次是python环境恢复：《解决：系统重装后的pip报错:Fatal error
in launcher: Unable to create process using》<br/> 最后是本文：《电脑升级总结系统重装后mongodb和redis重新恢复》

# 基本思路

1、下载新的数据库mongodb、redis,使用迁库工具进行迁库<br/> 2、不重新下载，进行恢复，重建path<br/> 最后选择第二种，感觉简单一点。

# 恢复mongo

第一步：将mongo的路径写入系统变量中（可能不写也没有关系）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020050913141359.png"/><br/>
第二步：尝试启动mongo,但是闪退<br/> 原因，没有data<br/> 解决：参照《解决mongodb的安装mongod命令不是内部或外部命令》

```
mongod --dbpath "‪J:\mongod\data\db"（ps:自己原来的路径）

```

会出现waitting for connections on port
27017<br/> <img alt="图片来自：https://blog.csdn.net/i10630226/article/details/46391111，因为自己的没有保存下来" src="https://img-blog.csdnimg.cn/20200509131836116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
此时，打开链接: [link](http://localhost:27017)
.可见<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509132013162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
即为正确启动，在pycharm的redis-sample中可见（这个集合mongo、redis的插件介绍可见《pycharm精选插件实测推荐—持续更新中》）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509132222614.png"/><br/>
即原来的数据

第三步：每次都去命令行启动非常麻烦，需要像之前一样设置为系统服务

设置命令：

```
mongod --bind_ip 0.0.0.0 --logpath  “J:\mongod\logs\mongodb.log”   --logappend  --dbpath     “J:\mongod\data\db” --port 27017 --serviceName "MongoDB"  --serviceDisplayName “MongoDB” --install （ps:路径换成自己的路径）

```

问题：此处遇到的问题在于设置服务的路径中不能有中文，否则启动时会出现错误2的提示，无法启动<br/>
原因应该就是路径中存在中文，因为在原本mongodb属性的可执行路径中的中文部分为乱码<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509132847678.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
原为乱码，现为已经改过来了！！！！！！！！！！

但是改过来后继续执行原来的命令

```
mongod --bind_ip 0.0.0.0 --logpath  “J:\mongod\logs\mongodb.log”   --logappend  --dbpath     “J:\mongod\data\db” --port 27017 --serviceName "MongoDB"  --serviceDisplayName “MongoDB” --install （ps:路径换成自己的路径）

```

会出现执行成功，但是系统服务处仍然是无法启动，可执行路径中的中文部分为乱码

解决：删除该系统服务后重新加入系统服务<br/>
删除系统服务，需要先禁止掉系统服务，原为自动执行，改为禁止即<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202005091331525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
然后找到win+r,输入regedit<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509133321435.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
去HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services
中找到mongodb<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509133649623.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
整个文件夹删除并重启

之后将改好的路径按照之前的命令再来一次

```
mongod --bind_ip 0.0.0.0 --logpath  “J:\mongod\logs\mongodb.log”   --logappend  --dbpath     “J:\mongod\data\db” --port 27017 --serviceName "MongoDB"  --serviceDisplayName “MongoDB” --install （ps:路径换成自己的路径）这次就会成功。

```

pycharm中就会显示<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509133840708.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

mongodb恢复成功

# 恢复redis

第一步：将redis路径加入path<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509134044455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第二步：进到Redis解压目录下，输入命令

```
redis-server --service-install redis.windows.conf

```

参见《Redis安装成windows服务》<br/>
进入Redis解压目录下的问题，cd后无法进入即不显示Redis解压目录，原因没有更换盘符（参见《使用cmd时cd命令失效》，在后面增加盘符即可，如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509134356719.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

系统服务添加成功：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509134615212.png"/><br/>
pycharm中也成功：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509134659920.png"/><br/>
内容也是原来的内容（以下是我爬取代理的内容）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509134742596.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

服务、数据均恢复

[1]https://blog.csdn.net/u010603823/article/details/52182679<br/> [2]https://blog.csdn.net/knqi007/article/details/78362510?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158899977319726869000748%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.57644%2522%257D&amp;request_id=158899977319726869000748&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2<sub>all</sub>first_rank_v2~rank_v25-1-78362510&amp;utm_term=redis+%E5%AE%89%E8%A3%85%E4%B8%BAWindows%E6%9C%8D%E5%8A%A1<br/> [3]https://blog.csdn.net/i10630226/article/details/46391111<br/> [4]https://blog.csdn.net/wyx_wx/article/details/76108662<br/> [5]https://blog.csdn.net/python__reported/article/details/105464104<br/> [6]https://blog.csdn.net/python__reported/article/details/105912954<br/> [7]https://blog.csdn.net/python__reported/article/details/106007143<br/> [8]https://blog.csdn.net/python__reported/article/details/106007143
