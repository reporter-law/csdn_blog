# 原创

： 《Python数据处理》9.1.2探索表函数笔记：print不输出期望值而是输出内存地址或者数据类型

# 《Python数据处理》9.1.2探索表函数笔记：print不输出期望值而是输出内存地址或者数据类型

### print输出内存地址或者数据类型

# 一、输出内存地址、数据类型

## （一）内存地址

```
a = 1
print(id(a))

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517205733185.png"/><br/> 直接输出内存地址是因为调用了id(）方法<br/> print()
方法在不调用id（）方法时不会输出内存地址

## （二）数据类型

但是有长得很像内存地址的数据类型<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517205949122.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
其中at
0x00这样的内容原本以为是内存地址的，试图通过内存地址来输出相应的值，参见《https://blog.csdn.net/ainu2919/article/details/102037350?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-4》

但是不行，因为这其实是数据的类型，这在xpath的使用中应该也遇到过

如果

```
node_7 = content_list.xpath('//i[@class="fraction"]')
return node_7

```

这样返回，没有text()<br/>
就会出现这样的数据类型<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517211427666.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

如果增加text()

```
node_7 = content_list.xpath('//i[@class="fraction"]/text()')

```

就可以正常输出<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517211704102.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
xpath中所要获得的值不能通过print直接输出xpath对象，需要使用xpath中的方法来获取相应的值

# 二、结论及解决之道

即使用特定数据结构时需要使用其特殊的输出方法,不能直接print

对于上述的agate模块的数据结构使用

```
print_table(max_columns=7)这个方法即可正常输出

```
