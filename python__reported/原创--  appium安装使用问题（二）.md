# 原创

： appium安装使用问题（二）

# appium安装使用问题（二）

### appium安装使用问题（二）

# 一、问题

## Appium安装问题

appium绝对不能直接安装，原因下载太慢<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525153504953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

使用node.js下载<br/> 要用appium就必须node.js,<br/>
下载node.js一路next的时候会有一个需要打勾的地方，注意不要打勾，因为这会安装python；当然对于还没有python的可以打勾勾上，如果有的就不要打勾<br/>
其次，对于不想将npm包安装到系统盘的，需要设置node.js的安装路径，推荐一个靠谱的方法

npm config set cache “F:\node_cache”<br/> npm config set prefix “F:”<br/> “”这个引号里面的就是想要安装的路径，随意设置即可<br/>
例如我的在node.js的盘里面新建了一个npm_packages文件夹<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525154220596.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## 第二步：问题一：

参照这个安装配置遇到了几个小问题，第一个问题就是win10配置java,安装专栏那里配置的环境变量，在cmd中打开时出现

```
'java' 不是内部或外部命令，也不是可运行的程序

```

或批处理文件。

输入java,javac都是一样的。

## 第三步：问题二：

相似的问题也在andrid-sdk中的aapt<br/> aapt的环境配置在上面那个专栏没有出现，在安装时是安装了的<br/>
即这个<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525151704192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
在build-tools,目录中<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525151723377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

在cmd中输入

```
aapt

```

如果出现

```
'aapt' 不是内部或外部命令，也不是可运行的程序

```

或批处理文件。<br/> 则存在问题

# 二、解决方法

## 第一个问题解决方法

这个问题一直没有解决，直到第二天才找到另一篇文章，<br/> 解决方法：<br/> 就是不需要配置classpath,<br/> 即环境变量配置为<br/> 变量名：<br/> JAVA_HOME<br/> 变量值：<br/>
要根据自己的实际路径配置<br/> I:\Program Files\Java\jdk-14.0.1

变量名：<br/> Path<br/> 变量值：<br/> %JAVA_HOME%\bin /<br/>
%JAVA_HOME%\jre\bin<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525151203929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525151244124.png"/><br/>
原因参见《java环境变量中classpath是必须配置吗》，链接: [link](https://blog.csdn.net/sinat_42483341/article/details/90418835?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159039039519724811842472%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&amp;request_id=159039039519724811842472&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v25-2-90418835.nonecase&amp;utm_term=java%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)
.

## 第二个问题的解决方法

第一步：配置环境变量

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525152151232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这有个前提就是要将ANDROID_HOME配置好<br/> 配置如下：

之后参照上图即可

第二步：重启电脑<br/> 刚刚配置好的环境变量，在cmd中输入仍然是

```
'aapt' 不是内部或外部命令，也不是可运行的程序

```

需要重启电脑才能成功，当然如果一步成功更好

# 三、环境变量配置完整图

andrid-sdk<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525152545647.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

java<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525152603742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

这两个需要新建

接下来的是path中的

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525152642638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525152706906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
该图下面的四个都是
