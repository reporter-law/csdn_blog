# 原创

： selenium弹窗之windows下载文件弹窗点击方法

# selenium弹窗之windows下载文件弹窗点击方法

### selenium弹窗之下载文件弹窗点击

# 一、弹窗类型

一般说到selenium中的弹窗包括以下三种类型：<br/>
类型一：窗口柄<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052814580515.png"/><br/>
这种窗口常说的就是窗口句柄，其实并不能算弹窗，应该属于窗口切换

类型二：web弹窗<br/> 使用如下命令导致的：

```
browser = webdriver.Firefox()

browser.implicitly_wait(0.1)
browser.get('https://www.bilibili.com/')
browser.execute_script('window.scrollTo(0,document.body.scrollHeight)')
browser.execute_script('alert("to botton")')

```

第三种：windows弹窗<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528150648136.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
参见《selenium+python自动化–文件下载弹窗处理(PyKeyboard)<br/> selenium+python自动化99–文件下载弹窗处理(PyKeyboard)
》，链接: [link](https://www.cnblogs.com/linlang781/p/9564148.html).

据这篇文章所述，这种弹窗并不是web界面的弹窗，我尝试过定位，确实不行，因为元素都找不到。因而这种弹窗我称之为windows弹窗，即不可以通过selenium的鼠标、键盘操作完成，用动作链也不行

# 二、windows下载文件弹窗点击方法

## pyuserinput模块

大部分文章对于这种弹窗的点击方法使用的是PyUserInpu模块

但是这个模块需要pyhook模块，但是这个模块pip无法下载，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151035271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

直接下载PyUserInput 也不行<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151212315.png"/><br/>
有解决下载的文章《https://blog.csdn.net/zhusongziye/article/details/79241410》，链接: [link](https://blog.csdn.net/zhusongziye/article/details/79241410).<br/>
具体怎么样没有尝试，一看就很麻烦

其中pyhook最新版本为2008年的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151441468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
pyuserinput也是2016年的了，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151550745.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
长时间没有更新，怕有许多问题就没有继续安装了

## pyautogui模块

在《python之鼠标、键盘模拟》，链接: [link](https://blog.csdn.net/qq_25360769/article/details/82590414?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=python%20%E9%BC%A0%E6%A0%87%E6%A8%A1%E6%8B%9F&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~sobaiduweb~default-2-82590414).<br/>
找到了这个pyautogui模块，最新版2020<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151731768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
近期更新的，一看比较靠谱，就用了这个模块<br/>
下载文件弹窗的点击方法<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528151946675.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528152007320.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

具体的点击位置需要慢慢调，我的弹窗解决方法<br/> 代码：

```
import pyautogui

pyautogui.moveTo(505,410)
pyautogui.click()
pyautogui.moveTo(765,465)
print('ok')

```
