# 原创

： pycharm加速（小结）以及后台任务缩减

# pycharm加速（小结）以及后台任务缩减

pycahrm启动加速的博文非常多<br/> 主要有：<br/>
1、清理缓存（增加启动速度以及防止运行卡顿）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408211047659.png"/><br/>
2、启动加速通过修改pycharm占用的xmx以及xms,xmx以及xms的文件在安装盘的bin目录下——（比如我的pycahrm安装在F盘的pycharm文件夹中，那么这个目录就是F:\pycharm\PyCharm Community
Edition
2019.3.3\bin），bin目录下有一个pycharm64.exe.vmoptions，不是64位的好像就是pycharm.exe.vmoptions这个文件。如下图：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408211645120.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
以记事本方式打开将Xms以及Xmx进行修改即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408211811433.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

3、运行加速即通过给予pycharm更多的内存空间，在帮助栏中打开编辑自定义vm选项<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408212034355.png"/><br/>
修改Xms以及Xmx即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408212116652.png"/><br/> 4、减少后台任务如index
,update skeleton等<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408210912797.png"/><br/>
index即文件索引的减少提高标记目录为排除<br/> scan update skeleton 可以通过文件\设置\外观&amp;行为\Notifications
中的log选项的√来减少<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408212624181.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200408212659724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
5、插件的禁止，包括系统插件与自己安装的插件<br/> 自己安装的无用插件可以自行卸载，而系统插件的禁用在帮助栏的Analyze Plugin Startup
Performance中，选择不需要用的插件即可，例如Github我就不需要用禁止即可
