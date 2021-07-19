# 原创

： python字典的遍历方式：向列表一样通过索引遍历字典的值

# python字典的遍历方式：向列表一样通过索引遍历字典的值

### python字典的遍历方式

# 一、常规遍历方式

参见：《python3
字典遍历操作》，链接: [link](https://blog.csdn.net/sxingming/article/details/51201258?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)
.

## （一）遍历字典的项

这和列表遍历一致：

```
dic = {'a':2,'b':3}
for item in dic.items():
	print(item)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200524114410305.png"/><br/> 格式为元组

## （二）遍历字典的键

第一种方法<br/> dic = {‘a’:2,‘b’:3}<br/> for i in dic:<br/> print(i)

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200524114713115.png"/><br/> 第二种方法：

```
dic = {'a':2,'b':3}
for i in dic.keys():
	print(i)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200524114719142.png"/><br/> 总结：效果一致，因为不加keys()默认就是遍历键

## （三）遍历字典的值

```
dic = {'a':2,'b':3}
for i in dic.values():
	print(i)

```

## （四）遍历字典的键值对

```
dic = {'a':2,'b':3}
for key ,value in dic.items():
	print(key,value)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200524115008519.png"/><br/> 看起来与遍历字典的项很像，但是前者是tuple元组类型，而后者为字符串

比较如下：

```
dic = {'a':2,'b':3}
for item in dic.items():
	print(type(item))
for key ,value in dic.items():
	#print(key,value)
	print(type(key),type(value))

```

# 二、向列表一样通过索引遍历字典的值

列表遍历：

```
list_ = [[1,2],[2,1]]
print(list_[0][0])

```

但是字典不能这样遍历，只能依据键来确定值，在某些时候就不方便<br/> 例如，在mongodb数据导出时不想导出_id而只想要内容<br/> 数据库中试图只要内容时就会出现问题，会将id的值一并纳入，但是不需要id的值

```
    for key,path in results[0].items():
    	print(path)

```

方法：<br/> 其实就是将item由元组变成列表，然后通过列表索引进行索引

```
list_ = []
for item in results[0].items():
    print(item)
    list_.append(list(item))

print(list_[1][1])

```

做这样的处理就是为了应对需要频繁确定键的难题，通过索引就不需要知道键而取值。

效果：通过索引来获取值，即知晓大概位置即可而不用确定键名，针对数据库的批量输出到控制台、以及批量输出具有重要意义。
