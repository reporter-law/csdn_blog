# 原创

： os模块遍历文件夹时的问题

# os模块遍历文件夹时的问题

### os模块遍历文件夹时的问题

# 一、遍历命令

```
    input_files = r"‪F:\360下载\firefox"
    for root, dirs, files in os.walk(input_files):
   		print(files)
    	for file in files:
    	print（file)

```

# 二、一共出现过三类问题

## 1、无反应

即pycharm执行时没有内容返回，但是也没有报错，就直接结束了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200622144250776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## 2、返回生成器

返回生成器内容

```
&lt;generator object walk at 0x0000024609604A20&gt;

```

返回生产器内容，那就遍历就行了或者使用list()，但是还是出现第一个问题即无反应

于是我就换了一个方法

```
print(os.listdir(input_files))

```

于是第三个报错来了

## 3、[WinError 3] 系统找不到指定的路径。

```
FileNotFoundError: [WinError 3] 系统找不到指定的路径。: '\u202aF:ð下载\x0cirefox'

```

这个问题就是盘符中存在其他内容，这个问题在之前复制路径输入cmd中也遇到过，去掉前面的空格即可，但是此处path均很紧密，没有空余可以去掉

```
input_files = "‪F:\360下载\firefox"

```

使用strip()方法可以去掉，即

```
print(os.listdir(input_files.strip()))

```

于是第四个报错来了

## 4、OSError: [WinError 123] 文件名、目录名或卷标语法不正确。

```
OSError: [WinError 123] 文件名、目录名或卷标语法不正确。: 'F:ð下载\x0cirefox'

```

这个就需要在path前增加一个r，即

```
input_files = r"‪F:\360下载\firefox"
print(os.listdir(input_files.strip("\u202a")))

```

成功

此时os.walk(input_files.strip("\u202a"))也可以了：

```
for root, dirs, files in os.walk(input_files.strip("\u202a")):
	print(files)

for file in files:
    print(file)
    break

```

# 三、总结

os模块读取路径时需要注意在路径中加“r",在路径内容中去掉多余的内容
