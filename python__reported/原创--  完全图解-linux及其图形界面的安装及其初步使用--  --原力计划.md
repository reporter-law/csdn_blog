# 原创

： 完全图解：linux及其图形界面的安装及其初步使用 ：

原力计划

# 完全图解：linux及其图形界面的安装及其初步使用

### linux及其图形界面的安装及其初步使用

成功界面：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202005211024192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521102451211.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

前言：<br/> 在csdn中常常看到程安利使用Linux，且据说相对于windows系统来说十分优越，windows弱爆了。<br/>
虽然如此，但是我还是没有下定决心使用Linux系统，因为重新学习一个系统比较麻烦，其学习耗时过多，能够用熟悉的系统就尽量用熟悉的系统。<br/>
然而，在学习过程中，主要是看书，大部分书中都会介绍程序在两种系统中的安装过程：linux和windows.<br/>
加上自己在windows升级中学会了系统安装，看到可以将linux系统安装在U盘中于是准备尝试一下linux系统的坑<br/>
参见：《将linux系统装入U盘，制作便携式linux系统》，链接: [link](https://blog.csdn.net/weixin_43136674/article/details/82419348?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158998291119725247630073%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&amp;request_id=158998291119725247630073&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v2~pc_rank_v3-2-82419348.first_rank_ecpm_v2_pc_rank_v3&amp;utm_term=linux%E5%AE%89%E8%A3%85U%E7%9B%98)
.

# 一、简要认识（非常重要）

## （一）Linux系统版本问题

linux系统有许多发行版本，与windows不同，不叫一个名字，例如windows10分为家庭版、专业版、企业版等，都叫windows只是版本不同，但是linux系统发行版本不一样，于是我就进入了第一个坑，在linux安装至U盘之类的目录下看到了centos6.5的iso镜像，一脸懵逼，我不是来安装Linux系统的吗？，怎么都出现了centos,这是一个系统吗？还是在教我安装另一个操作系统！！！！！！

上网搜索Linux系统，发现其版本有不同的名字<br/> 例如Ubuntu,
centos等<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520220403113.png"/>

## （二）VMware虚拟机

官网：链接: [link](https://www.vmware.com/cn.html).一看，没有叫做VMware虚拟机的软件啊！！<br/>
其下载界面为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520220814862.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
不知道下载哪一个？<br/> 之后，就在腾讯电脑管家中搜索找到<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520220746752.png"/>
VMware虚拟机官方名称叫做：VMware Workstation<br/> 这个也有两个版本：VMware Workstation 15 Player、VMware Workstation Pro<br/>
前者免费，后者只可以试用，自然是前者呢？

# 二、安装过程

## （一）安装centos哪一个版本

在Linux官网中只有centos8的版本，安装最新的自然OK，于是用迅雷x下载了

但是在安装时出了问题，第一个问题是vm版本不支持centos8，最高只有centos7，因为用腾讯电脑管家下载的，比网页直接下载快，但是这个下载的是VMware Workstation 14
Player<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520221553222.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

最高仅支持centos7<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520221652635.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

于是我去官网下载了VMware Workstation Pro，但是不知道为什么无法启动，提示我缺失了某个dull，说重新安装。重新安装，你想个屁呢？VMware Workstation
Pro安装时间特别长，差不多10分钟，那肯定不能啊！<br/> 于是我就又下载了VMware Workstation 15 Player，这个安装比较快，大概1-2分钟就搞定了，但是还是无法启动

既然不支持VMware Workstation 15 Player、VMware Workstation Pro，那就重新下载了VMware Workstation 14 Player。<br/>
然后下载centos7,下载地址：链接: [link](http://www.linuxdown.net/CentOS/2017/0107/9018.html).

此处有镜像，自然下载镜像的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520222206766.png"/>

选择了阿里云的镜像，链接: [link](http://mirrors.aliyun.com/centos/7/isos/x86_64/).<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520222236322.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
又是一堆版本，那就看看0_README.txt<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520222331540.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
选择第一个版本即CentOS-7-x86_64-DVD-2003.iso

下载下来大概也得半个小时，注意最好下载到固态硬盘中，因为迅雷X10M/S的速度写入机械硬盘会报错误，就是磁盘空间已满之类的，一直停留在99.9%

## （二）安装过程

不要参照其他教程，其他教程下可能需要安装特定的VMware Workstation 版本，这个可把我给找死了，发现完全不同于这些教程。<br/>
这个是安装好了的：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520222809885.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
正式安装过程如下图：

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520222935104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
ps:注意此处选择自己的U盘，例如：

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223026471.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223052916.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223106728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

进入自定义硬件设置<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223129566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
选着新CD<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223152249.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
浏览到自己下载的centos7的位置<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223238317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

选择USB控制器，更改U盘兼容3.0<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223331670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223352315.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

点击完成即可

之后打开虚拟机<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223436650.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
进入安装过程，一路next即可<br/> 注意在密码和用户那里不要管，不然容易出问题，<br/> 特别是密码，之前建了一个，结果无法输入，据说不能用小键盘输入数字，需要且只能使用上面的数字输入。我之前没有找到这个方法，直接卸载了<br/>
卸载方法：选中centos7,右键点击，选择从磁盘中删除即可

# 三、启动

## （一）第一步：点击播放虚拟机

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520223906766.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
进入选择界面，不要管就可以了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052022400233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052022392025.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## （二）第二步：输入用户名，密码

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520224031209.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
初始的都是root,但是密码需要重设，因为没有设置密码，当然也可以在安装时设置

密码重置可以参加《linux在安装过程中未设置root密码的解决方法》，链接: [link](https://blog.csdn.net/annita2019/article/details/103554640?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158998581419724848346685%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&amp;request_id=158998581419724848346685&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v25-1-103554640.nonecase&amp;utm_term=linux%E5%AE%89%E8%A3%85%E8%BF%87%E7%A8%8B%E4%B8%AD%E6%9C%AA%E8%AE%BE%E7%BD%AE%E5%AF%86%E7%A0%81)
.

进入后是命令行模式，密码输入无反应不要紧张，就是这样的，你已经输入了

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520224504474.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> **
只有root才可以！！！！！！！！**<br/> **只有root才可以！！！！！！！！**<br/> **只有root才可以！！！！！！！！**

只有在root用户中才可以下载图形界面系统，换成熟悉的图形界面<br/> 参见《centos 7
启动与切换图形界面》，链接: [link](https://blog.csdn.net/kswkly/article/details/83690565?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158998600119724848344015%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&amp;request_id=158998600119724848344015&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~baidu_landing_v2~default-2-83690565.nonecase&amp;utm_term=centos%E5%9B%BE%E5%BD%A2%E7%95%8C%E9%9D%A2).<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200520224809431.png"/>

## （三）出现错误

第一个错误为：

```
 yum 出现could not retrieve mirrorlist 

```

按照csdn上的解决方案，如：《Centos7 yum 出现could not retrieve mirrorlist
最终解决方案》，链接: [link](https://blog.csdn.net/jackiesimpson/article/details/80200578?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-1)
.

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33

```

就会出现另一个报错

```
vim:command not found

```

解决方法：参见《解决centos vim:command not found 和 yum -y install xxx失败
的问题（联网问题）》，链接: [link](https://blog.csdn.net/qq_38214193/article/details/81114445?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159002343219724811864619%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&amp;request_id=159002343219724811864619&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v2~pc_rank_v3-2-81114445.first_rank_ecpm_v2_pc_rank_v3&amp;utm_term=centos7+vim+command+not+found).等<br/>
基本思路就是安装vim,

```
yum -y install vim-enhanced

```

****但是问题来了！！！！！！！！！！！！！****

解决第一个报错需要联网，因为需要联网而下载vim,这不是自相矛盾吗？<br/> 找遍了博文，终于发现有的是：

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33
还有的是：
vi /etc/sysconfig/network-scripts/ifcfg-ens33

```

这两个咋一看就是一样的啊！后者或许是前者的缩写，但是并非如此<br/> 猜测：可能vi是自带的工具、vim是需要自行安装的类似工具，所以许多不同的解决方法才能够都出现，当然也可能是抄的不够认真。

通过vi
/etc/sysconfig/network-scripts/ifcfg-ens33进入后的另一个问题，就是无法编辑，无法改为yes,因为输入没有反应。这个问题在其他解决方法中也存在，例如通过修改dns来解决没有联网的问题，基本都会进入这个界面<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052110210492.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
修改为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521095002717.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

修改方式：

无法修改，不知误触了什么可以修改，但是wq保存不会，直到找到了这一篇文章《CentOS7（Linux）怎么保存退出vi/vim编辑》，链接: [link](https://blog.csdn.net/qq_29964641/article/details/87161461?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=centos7%20vim%20%E6%80%8E%E4%B9%88%E4%BF%9D%E5%AD%98%E9%80%80%E5%87%BA&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-87161461)
.

快捷键 i 进入，（前面没有空格，只是为了凸显i的存在），进入后会出现inset，在最下方，然后可以修改为yes,之后按下ESC

输入:
wq,enter即可退出<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521100101657.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521100138640.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 四、安装图形界面

## （一）安装过程

我是先安装 GNOME Desktop

```
yum groupinstall GNOME Desktop

```

然后安装 X Window System

```
yum groupinstall “X Window System”

```

效果一样，但是使用

```
startx

```

无法启动（后来可以，原因在于x与start不能有空格）

而是

```
init 5 

```

才可以启动

## （二）问题

一开始只是方框界面，不知道是什么语言。

后来换成英语界面；没有中文界面，找不到汉语，只能使用英语界面<br/>
更换方法：应用&gt;系统工具&gt;设置&gt;语言<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521100758148.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521101116607.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521101238720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521101308986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

找不到汉语

其实感觉与安卓系统很像，似乎安卓是基于linux（好像在哪里看到过这个说法，但是并不确定）

****以上就是全部！！！！！！！！！！！！！！！！！****
