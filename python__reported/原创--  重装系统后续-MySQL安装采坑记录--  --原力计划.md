# 原创

： 重装系统后续：MySQL安装采坑记录 ：

原力计划

# 重装系统后续：MySQL安装采坑记录

### 重装系统后续：MySQL安装内容

# 一、MySQL内容介绍

MySQL安装的几种模式：

Developer Default：提供一种安装类型，其中包括所选版本的MySQL服务器以及其他与MySQL开发相关的MySQL工具，例如MySQL Workbench。

Server Only: 不使用其他产品为选定版本的MySQL Server提供设置

Custom：使您能够选择任何版本的MySQL
Server和其他MySQL产品。.<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510092928566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
推荐的都是Developer Default<br/> 但是我仅使用python操作MySQL，而且用pycharm的可视化插件，所以安装的其他的一些操作软件就有些多余

# 二、选择：推荐安装

推荐的都是Developer Default<br/> 但是我仅使用python操作MySQL，而且用pycharm的可视化插件，所以安装的其他的一些操作软件就有些多余，因为几乎不用。<br/> 例如：MySQL
Workbench。<br/> 图片源自：《MySQL：MySQL
Workbench的使用》—url:https://www.cnblogs.com/hahayixiao/p/9849742.html<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510093413337.png"/>

之前下载的时候用过一次，其实就是一个可视化的操作MySQL的软件，我一般在pycharm中用，所以这个可视化的操作MySQL的软件几乎用不上，安装上去显得软件特别多，心里添堵，所以推荐仅安装Server Only

如果需要MySQL Workbench，也可以自行安装不是更好，安装路径：https://downloads.mysql.com/archives/workbench/<br/> 安装过程参照：《Mysql Server 8.0.11
安装教程（踩坑教学）》,链接: [link](https://blog.csdn.net/zhangzhetaojj/article/details/80684306?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)
.

# 三、重装系统遇到的问题：

## 一、the requirement is still failing

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510094554620.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510094605800.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是我的python明明是python3.7且可以用<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051009465458.png"/><br/>
但是这个python并不是重装的，而是对于原来win7系统中的python3.7进行的恢复，这种恢复遇到了许多问题，这就是其一。

后来发现和这个没有关系！！！！！！！！

## 二、安装mysql-for-visualstudio-1.2.9

下载地址：https://www.softpedia.com/get/Programming/Other-Programming-Files/?utm_source=spd&amp;utm_campaign=postdl_redir

但是直接安装不行，会报错。因为依赖于visualstudio<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510100822126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

安装Visual
Studio<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510100859816.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
安装过程：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510100941243.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510100959370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510101145934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
可以选着配置安装路径以及缓存路径。<br/>
注意可以不用选着这个选项，选着了会下载一堆东西，占空间，只要下载好基本的东西即可，这里面的什么都不要选，除非你需要。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510101405212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510112604199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 四、安装MySQL

## （一）安装内容

下载好了以后就可以进入安装，选择Server
Only:<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510112456353.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510125849854.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051012592120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510130009328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510130025926.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510130036208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
填好密码<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202005101301451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510130154855.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## （二）遇到报错

遇到报错：MySQL error 1042: Unable to connect to any of the specified MySQL
hosts.<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510113114381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510113126217.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
解决方法：

由上面报错可知。Unable to connect to any of the specified MySQL hosts<br/>
那就connect即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510130405831.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

进入此电脑/管理/服务，选择MySQL80，右击属性，将之改为本地系统账户<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131146474.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131242519.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
然后应用即可<br/>
回到安装选项中<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131328606.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
选择执行（execute）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131426594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202005101314185.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131440847.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510131454382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## 三、安装成功后的坑

第一个坑：

```
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

```

据说要修改my.ini这个文件，一看挺麻烦的就没有修改试图在DB brwser中不使用账户与密码直接登录，此时报错时区不对，进而修改了my.ini添加

```
default-time_zone = '+8:00'

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510141959265.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
参见《修改MySQL的时区，涉及参数time_zone》

第二个坑：

之后出错：本地计算机上的mysql服务启动停止后,某些服务在未由其他服务或程序使用时将自动停止<br/>
图片来源：《本地计算机上的mysql服务启动停止后,某些服务在未由其他服务或程序使用时将自动停止》，链接: [link](https://blog.csdn.net/qq_26525215/article/details/53424152).<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510142249245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
按照《MySQL 服务正在启动 . MySQL 服务无法启动 服务没有报告任何错误 解决方案》第三种方法终于解决了，前两种均无法解决。<br/> 前两种会报错

```
MySQL 服务正在启动 . MySQL 服务无法启动 服务没有报告任何错误

```

然而即使如此，这条不需要密码的路走不通<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510142739786.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510142817234.png"/>

走这条路的原因：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510142904946.png"/><br/> 不输入密码能够进入，<br/>
显示：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510153110907.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## 注意

仔细查了一下pycahrm中Dan Cioca：Database
Navigator，发现许多人报这个问题<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511082750520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
可能哪里有些不支持！！！！

之后重装mysql时仍然这个错误，但是可以登录进入<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511082905180.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
不过这可能是因为登录时没有选着本地系统账户，而是网络账户即没有出现前面的错误！<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511083000847.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
此外用mysql的可视化软件是可以查看的，只是pycharm中的Database Navigator一直报错

## Database Navigator报错解决方法

参见《【已解决】Android Studio中Database
Navigator插件连接mysql建立失败：时区问题》，链接: [link](https://blog.csdn.net/qq_32682301/article/details/100537869).<br/>
不从mysql处建立连接，而从custom处<br/>
即<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511135002753.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
输入

```
jdbc:mysql://localhost:3306/mysql?serverTimezone=UTC

```

修正时区即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511135022235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511135223338.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
Database Navigator操作起来有些麻烦，没有mongo容易操作，不过mysql本来就比mango难操作一些！！！！1
