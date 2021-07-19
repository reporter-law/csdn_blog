# 原创

： 解决：系统重装后的pip报错:Fatal error in launcher: Unable to create process using

# 解决：系统重装后的pip报错:Fatal error in launcher: Unable to create process using

### 系统重装后的pip

```
python -m pip install --upgrade pip

```

后成功。

第二次重装系统，一样的问题，更新命令无法解决，遇到

```
Fatal error in launcher: Unable to create process using '"e:\users\administrator\appdata\local\programs\python\python37\python.exe"  "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\pip3.exe" ': ???????????

```

按照博主《解决"pip Fatal error in launcher: Unable to create process using … "的错误》在633行进行修改后报错：

```
该版本的 D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\pip.exe 与你运行的 Windows 版本不兼容。请查看计算机的系统信息，然后联系软件发布者。

```

当初下的就是64位的python3.7，进行与win10 64位不兼容！！！！！！！！

解决方法：<br/> 1、卸载pip

```
python -m pip uninstall pip

```

2、安装pip<br/> 《Windows下的Python安装pip，及使用技巧》

```
python setup.py install

```

此命令加wheel的位置报错找不到setup.py

```
can't open file 'setup.py': [Errno 2] No such file or directory

```

失败！！！！！！！！！！！！！！！！！！！！！！！！！！

3、最终解决：pycharm<br/> 可以进入pycharm的项目解释器中，点击+，就会出现点击不了的现象，接下来会提示你

```
python package tools not found

```

存在一个可安装的packaging,点击安装即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509085640802.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
成功后就会出现packaging<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020050909002987.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509090046112.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200509090120970.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
