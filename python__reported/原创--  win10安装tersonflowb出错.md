# 原创

： win10安装tersonflowb出错

# win10安装tersonflowb出错

### win10安装tersonflowb出错

# 一、报错

通过查找，发现第一个报错内容为

```
ERROR: Failed building wheel for wrapt.......
Running setup.py clean for wrapt...........
Failed to build wrapt.......
#此处为简写，大体该报错的关键内容如上

```

# 二、解决方法

## （一）有效

链接: [win10 安装tensorflow 报错“ERROR: Failed building wheel for wrapt”解决办法](https://blog.csdn.net/m0_37864814/article/details/103055869)
.

就是下载该模块此处为”wrapt"的whl文件，链接: [wrapt](https://www.lfd.uci.edu/~gohlke/pythonlibs/#wrapt).

注意此处可能存在一定的网络延迟，我第一次看到这个方法时，ctrl+F去搜索时只有一个命中目标，在前面<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200706093047757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是在里面没有找到wrapt,点击这个长时间无法进入，这应该是网络的原因，后来网络好了，下载成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200706093209659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
安装成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200706093222815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
tersonflow安装就也成功了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200706093301259.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## （一）无效（只是对我无效）

1、<br/> pip install wrapt --ignore-installed<br/>
出自链接: [Tensorflow安装错误之 Cannot uninstall wrapt](https://blog.csdn.net/weixin_41923658/article/details/96127770?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-1).<br/>
后来仔细看了一下，好像不是同一个错误，但是这个错误在我的里面似乎也有，不过可能是两个错误夹在一起？？

2、直接安装源码<br/> github上下载，链接: [GrahamDumpleton](https://github.com/GrahamDumpleton/wrapt/releases/tag/1.12.0).<br/> 一样安装不了

特此记录！！！！！！！！！！
