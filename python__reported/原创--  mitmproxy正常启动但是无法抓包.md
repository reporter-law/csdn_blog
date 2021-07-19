# 原创

： mitmproxy正常启动但是无法抓包

# mitmproxy正常启动但是无法抓包

### mitmproxy正常启动但是无法抓包

# 一、现象

mitmproxy正常启动是指，cmd中出现了

```
Proxy server listening at http://*:8080
Loading script J:\PyCharm项目\项目\项目四_mitmproxy_and_email\addon.py(ps:正常导入脚本）

```

但是没有这个界面

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200522090650533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
而是<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200522090712566.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、原因

查询方法：

## （一）第一步：

确认系统证书；<br/> 确认手机证书；<br/> 确认代理正确<br/> 这些问题是初步设置，基本都是正确的，因为之前使用的时候是正确的

## （二）第二步：重点在端口

### 1、ip错误

系统证书和手机证书安装了基本不用确认，主要是确认代理正确与否

尝试ping自己的ip<br/> cmd中<br/> ipconfig<br/> 查询ip<br/> 在此处时一般也不用在意，前提是发现错误时，没有更改<br/> 而在这里发现错误，我重新设置了代理，结果填错误，ping的时候才发现

```
ping (ip)

```

出现“请求超时”的字样，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200522091821618.png"/>

当时我就很诧异，怎么会请求超时，由于我是校园网，于是重新登录了一遍，但是正常上网啊！直到再次在网络中寻找时发现有本地连接、以太网，ip还各不相同，于是尝试更换了发现自己的ip填错了

改回ip后重新ping,就会出现下面的正常数据<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200522091902164.png"/>

### 2、端口

ip改回来后仍然是没有这些数据的返回，说明数据没有通过代理<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200522092016720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

又找了一段时间错误，偶然更改端口时发现突然又可以

```
mitmdump -p 8088

```

再次换回8080时又没有了，说明可能是端口有问题，8080端口可能被占用了，与其他人的或者自己的存在冲突

这种问题简直令我惊讶，找遍了问题竟然是这种小失误，或许偶尔需要随便试试最简单的方法

这种问题还是第一次遇到，特此留证！！！！

仔细找了一下，发现确实是端口被占用了，自己的程序占用了。因为我在任务计划程序中已经运行着mitmdump,所以在命令行再次运行时无反应！！！！！！！！！！！！！！！！
