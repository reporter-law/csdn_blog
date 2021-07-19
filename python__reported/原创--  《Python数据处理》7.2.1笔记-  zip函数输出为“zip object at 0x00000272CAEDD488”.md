# 原创

： 《Python数据处理》7.2.1笔记:  zip函数输出为“zip object at 0x00000272CAEDD488”

# 《Python数据处理》7.2.1笔记:  zip函数输出为“zip object at 0x00000272CAEDD488”

### 《Python数据处理》7.2.1笔记:zip函数输出为“zip object at 0x00000272CAEDD488”

# 一、现象

书中位置：2合并问题与答案的 第三个代码处：

```
#变量名有不同，原为zipped_data
zip_data = []
for drow in  new_data:
    zip_data.append(zip(head_row, drow))
   #作者是直接打印的
   zip_data[0]

```

但是直接打印的内容是

```
&lt;zip object at 0x000001B2B4BD2F08&gt;

```

将之进行遍历：

```
&lt;zip object at 0x000001B2B4BD2F08&gt;
&lt;zip object at 0x000001B2B4BD2FC8&gt;
&lt;zip object at 0x000001B2B4BD40C8&gt;
&lt;zip object at 0x000001B2B4BD4188&gt;
&lt;zip object at 0x000001B2B4BD4248&gt;
&lt;zip object at 0x000001B2B4BD4308&gt;
&lt;zip object at 0x000001B2B4BD43C8&gt;

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512182822991.png"/><br/> 返回zip对象而不是内容

# 二、原因

参考《python中使用zip函数出现》,原因是为了节约内存，python3基于此对此进行了优化，输出只输出对象的内存位置而不打印出来。而在python2中可以直接输出到屏幕

# 三、解决办法

## （一）增加一个list（）

```
for data in zip_data:
	print(list(data))

```

但是这样输出与书中不一致，且不够美观<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512183431940.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

## （二）进行美化

代码：

```
import pprint
for data in zip_data:
	pprint.pprint(list(data))

```

美化后：

```
	(['TN12_3',
'Person 3 who slept under net',
'Who slept under this mosquito net last night?'],
 'NA'),

```

至此，与书中一样了！！！！！！！！！！！
