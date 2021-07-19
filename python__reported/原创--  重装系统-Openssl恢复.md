# 原创

： 重装系统：Openssl恢复

# 重装系统：Openssl恢复

### 重装系统：Openssl恢复

# 一、现象

运行scrapy时遇到报错

```
twisted.web._newclient.ResponseNeverReceived: [&lt;twisted.python.failure.Failure OpenSSL.SSL.Error: [('SSL routines', 'ssl3_get_record', 'wrong version number')]&gt;]

```

重装系统前是没有这个问题的，重装系统后遇到了，pyopenssl一直安装着，

# 二、原因

就是该有的模块存在缺失<br/> 第一步、因而首先进行了scrapy框架的更新看看能否解决

```
pip install --upgrade -i https://pypi.douban.com/simple scrapy

```

没有装wheel,装上即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141249767.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
不过这是一个比较奇怪的事前，在写文章前已经更新过了，再更新一次一应该是

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141408186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
不知道为什么是这样，不过没关系，装上即可<br/> pip install --upgrade -i https://pypi.douban.com/simple wheel<br/>
装上后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141440436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

然而，问题没有解决，直接打开OpenSSL出现了这样的情况<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511140459339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

第二步、重装OpenSSL<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141536367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

一路next<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141625665.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141638572.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
不选择也可以完成

环境变量已经有了OpenSSL<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511141824565.png"/>

重装后仍为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511142548283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、解决方法

## （一）下载：msvcr120.dll

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511142629825.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
再次报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511142716637.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## （二）下载diretx修复工具继续修复

注意是diretx修复工具，不是diretx9.0<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511143946308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

<img alt="无法解决" src="https://img-blog.csdnimg.cn/20200511144152679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511144227762.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 四、成功
