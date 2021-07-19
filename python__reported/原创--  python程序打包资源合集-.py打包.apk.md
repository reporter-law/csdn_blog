# 原创

： python程序打包资源合集：.py打包.apk

# python程序打包资源合集：.py打包.apk

### python程序打包：.py打包.apk

# 一、说明

程序打包：<br/> python程序打包与kivy关系不大，python程序打包就是类似于利用pyinstaller将python程序打包为windows可执行的程序，即.py转变为.exe.

程序制作：<br/> .py打包为.apk就是与上述内容一样，而kivy是制作app即.apk的模块，类似于pyqt、tkinter这样的

kivy:<br/> 然而这两者是有关的，即kivy制作的python程序才能够使用上述程序打包为.apk,即一般说的kivy=tkinter(pyqt)+pyinstaller

# 二，打包过程

环境安装：<br/> 1、链接: [天翼云盘](https://cloud.189.cn/t/EbmyaaJV3yUv).(访问码:iww8)<br/> 天翼云盘下载快些，但是需要注册一个，直接微信登录即可

2、不想注册慢点，链接: [百度云盘](https://pan.baidu.com/s/1F3n1fblLuptxd_QVcG870Q).，提取码：kivy<br/> 安装过程参见：&amp;凌云木：Python
kivy打包apk笔记，链接: [Python kivy打包apk笔记](https://blog.csdn.net/qq_43551034/article/details/104873485).<br/> 环境命令：

```
buildozer init
#（初始化：不过可以不用，因为初始设置已经搞定了，即后两个命令即可）
gedit buildozer.spec
（生成.spec文件）
buildozer android_new debug
（打包命令）

```

3、打包测试资源<br/> 这个是kivy编程的一本书的源码，链接: [link](https://github.com/mvasilkov/kb/tree/master).
