# 原创

： 《python3网络爬虫开发实战》学习笔记：splash无法进入

# 《python3网络爬虫开发实战》学习笔记：splash无法进入

为了能够在中断远程服务器后依然能够运行splash,使用命令 docker-d -p 8050:8050 scrapinghub/splash
进行安装<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200313220514382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
在输入http://localhost:8050无法打开splash,然后参照《docker端口映射后不能使用localhost:port访问》将之修改为http://192.168.99.100:8050仍
然不能打开，换了其他浏览器以及重启之后也是如此。<br/> 最后我想可能是安装没有成功，使用命令docker run -p 8050:8050
scrapinghub/splash,再次进行安装后成功。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200313220956791.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
需要出现上述界面才是安装成功，之后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200313221052865.png"/>
