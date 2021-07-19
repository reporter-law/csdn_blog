# 原创

： Pycharm：Plugin "better-mybatis-generator" is incompatible (supported only in IntelliJ IDEA)

# Pycharm：Plugin "better-mybatis-generator" is incompatible (supported only in IntelliJ IDEA)

### Pycharm：一直报插件错误

# 一、现象

每次打开pycharm,都会报插件错误，特别烦

```
插件错误: Plugin "better-mybatis-generator" is incompatible (supported only in IntelliJ IDEA).

```

# 二、寻找原因

插件中并没有我之前下载的

```
Plugin "better-mybatis-generator"

```

试图去插件安装位置找到并删除，但是不知道安装在哪里，通过everything找到了，这是一个非常讨厌的事，一直装在C盘，使用各种方式禁止软件装在C盘都没有用，不论更改注册表还是去window应用安装位置更改安装目录以及自定义安装目录都没有用<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511084741599.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、解决方法

删除后重启就不会报错了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511085007115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

重启后没有报错了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200511085055444.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
