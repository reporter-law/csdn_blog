# 原创

： win32com报错filenotfound

# win32com报错filenotfound

### win32com报错filenotfound

# 一、报错

# 二、原因

由于将py文件转到了其它盘的位置以及原系统的temp存在盘改变<br/>
即新内容存储位置改变了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200705143109890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这个是修改完成的<br/> 原来的报保存位置再E盘，原E盘出了问题，且由于我将存储服务禁用了导致原存储位置即E盘由于存储服务禁用导致没有更改过来，所以报这个错误<br/> 这种情况下此处存储现象应该显示：<br/>
管理员在电脑上禁止使用存储服务<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200705143604984.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
图片来源：链接: [想要更改新内容的保存位置但是存储里面显示的是，管理员已在此系统上禁止存储服务，该怎么解决呢？<br/> ](3C415EA7B7A695747646EA6D13D01CA2.1592215725487).

按照此处链接方法是无法解决该问题的

# 三、解决方法

打开Storage
Service并启动<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200705143806938.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200705143913772.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
