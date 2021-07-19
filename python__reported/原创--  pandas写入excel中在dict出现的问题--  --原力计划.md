# 原创

： pandas写入excel中在dict出现的问题 ：

原力计划

# pandas写入excel中在dict出现的问题

### pandas写入excel中在dict出现的问题

# 一、目标

对写入的数据设置为集合套集合的格式<br/> 如：

```
a={"a":{"b":"c"}

```

这样的集合在for循环结构中，即希望在for循环中出现自己需要的数据则可以进行相应的变更

程序如下：

```
 with open("情节.txt", "r", encoding="utf-8")as f:
        condition = f.readlines()
        for i in condition:


            tuple = process.extractOne(i.strip("\n"), text2)
            # print(list(tuple))
            if list(tuple)[-1] &gt;= 90 and tuple[0] != "犯罪":
                element = list(tuple)[0]
                print("字符串模糊匹配的前几位为： ", element)
                if element + "\n" in condition:
                    print("在的： ",element)
                    element_list[title] = 1
                    dataframe[i.strip("\n")] = element_list
                else:
                    element_list[title] = 0
                    dataframe[i.strip("\n")] = element_list

```

在最后这段if-else的条件判断中就是试图实现自己上述的目标，如果符合条件则将集合中的内容设为1，否者设为0

# 二、问题

从逻辑上没有发现问题，单个输出时即没有else时，也没有问题<br/> 但是一旦存在else时，就会出现覆盖的问题，即后续内容会覆盖前面的内容，原因直到现在都没有找到

一旦匹配成果就会全部更新<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627174933168.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

没有匹配成果<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627174957632.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
最终结果则全部被覆盖<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175034849.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175051566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175107566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020062717511871.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、解决方法

尝试过许多方法都没有办法解决，直到最后用来一个比较复杂的方法，就是先将内容全部设为0，然后对这个全部设为0的集合进行更新

```
"""两个集合以便更新，直接似乎无法更新"""
    for i in condition:
        element_list[title] = 0
        dataframe[i.strip("\n")] = element_list

    for i in condition:
        tuple = process.extractOne(i.strip("\n"), text2)
        if tuple[1]&gt;90 and tuple[0] != "犯罪":
            print("存在的量刑情节： ", tuple[0])
            element_lists[title] = 1
            dataframes[tuple[0]] = element_lists
dataframe_ = dict(dataframe,**dataframes)


for i in condition:
        element_list[title] = 0
        dataframe[i.strip("\n")] = element_list
  是先全部设为0的集合

```

这个是匹配时得到的集合

```
 for i in condition:
        tuple = process.extractOne(i.strip("\n"), text2)
        if tuple[1]&gt;90 and tuple[0] != "犯罪":
            print("存在的量刑情节： ", tuple[0])
            element_lists[title] = 1
            dataframes[tuple[0]] = element_lists

```

结果为：<br/>
全部设为0时：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175659743.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

匹配到的：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175729459.png"/>

最后更新后的：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200627175935574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 四、结语

虽然最后成功了，但是始终不明白之前的想法为什么不行！！！！
