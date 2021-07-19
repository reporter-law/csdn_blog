# 原创

： Django项目部署

# Django项目部署

### Django项目部署

# 一、成果结果

PC端<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731081054257.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
手机上：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731081309496.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、部署过程

## （一）项目来源

个人博客使用django制作的，原本我是在学习《python编程：从入门到实践》中完整的写完了，准备部署的，但是由于heroku注册的验证码需要搭个梯子，由于找合适的梯子（主要是免费的原因）而放弃了。由于各种原因导致原来写的django被删除了，所以本次的django项目是直接拿的别人的，这个项目来源于Github上的mazixiang,<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731082208360.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
就是这位大神

## （二）项目修改

主要是对项目的格式以及文字等作了一些调整，整体的框架以及设计都没有改动。项目在本地运行，可以直接在虚拟环境（直接用pycharm新建的项目就是运行在虚拟环境中，直接activate即可激活）中下载django和django-bootstrap3即可，但是在这里被这两个东西的版本卡了一天，因为我的python版本是3.7.0的，在本地打开的时候一直报错，要么直接报哪里哪里错误，要么是A
server error occurred. Please contact the administrator.

其实这些都是django和django-bootstrap3的版本不对，亲测好用的版本为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020073109402452.png"/>

## （三）项目部署路径

就我所知，免费的项目部署方式有heroku、pythonanywhere<br/> heroku部署：<br/>
heroku官网有详细教程，例如<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731094221518.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
我的在这一步走不下去了，因为出现了Scaling dynos… ! ! Couldn’t find that process type (web)
.暂时没有找到解决方法<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731094253549.png"/><br/>
pythonanywher部署：<br/> 参见《使用PythonAnyWhere和GitHub免费部署Django网站》，都是按照这个来的，虽然是2019-01-01的，但是仍然可以用

# 三、部署成功

应该类似于借了个计算机给你用，然后让本地上运行的程序可以长期运行，<br/>
可用配置为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731094652558.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
期限限制为三个月登录一次<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200731094847199.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
