# 原创

： 《python数据分析基础》：[Errno 11004] getaddrinfo failed

# 《python数据分析基础》：[Errno 11004] getaddrinfo failed

《python数据分析基础》第6.4 seaborn的第三个图“成对变量之间的散点图与单变量直方图”

```
'''成对变量散点图和单变量直方图'''
iris = sns.load_dataset('iris')
sns.pairplot(iris)

```

在写这个代码时就存在一个疑惑，这个图的代码怎么没有数据或者说值，其他的可视化的图都会有值的导入，即使没有现成数据，也会使用pandas进行随机生成，例如

```
mean, cov = [5, 10], [(1, .5), (.5, 1)]
data = np.random.multivariate_normal(mean, cov, 200)
print(data)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430134249102.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是这里的不存在值，后来发现这个值是通过网络连接seaborn-data导入的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430134500991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020043013451872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
而在此处就遇到了这个问题<br/> 当我使用plt.show()时出现报错

```
urllib.error.URLError: &lt;urlopen error [Errno 11004] getaddrinfo failed&gt;

```

指向requests.py的第1319行

```
File "C:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\urllib\request.py", line 1319, in do_open
raise URLError(err)

```

原本以为是seaborn与requests之间对于方法名称的不一致，但是requests一直在用都没有问题，而报错中没有提到seaborn的错误，其错误直接指向requests<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430134655923.png"/><br/>
于是我对requests.py进行了修改，将raise URLError(err)注释掉并添加pass

```
        try:
        try:
            h.request(req.get_method(), req.selector, req.data, headers,
                      encode_chunked=req.has_header('Transfer-encoding'))
        except OSError as err: # timeout error
            pass
            #raise URLError(err)
        r = h.getresponse()
    except:
        h.close()
        raise

```

但是没有效果，报错：

```
AttributeError: 'NoneType' object has no attribute 'makefile'

```

经过网上查找，发现许多文章都说[Errno 11004] getaddrinfo failed 是dns的问题，于是我想到之前看到的，seaborn的值值是通过网络连接seaborn-data导入的，因而是不是有可能是在requests
seaborn-data时网络的问题或者是被屏蔽了。被屏蔽了就要解除屏蔽。解决屏蔽的方法很简单（但是这个垃圾网站审核不能通过！！！！）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430135642635.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

然而，当我重新测试时有突然可以了，所以可能不是被屏蔽了，而是网络、代理、dns之类的问题。<br/>
但是，我再次制作箱线图时，又出现了这个问题，一模一样的报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430141127930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
还增加了两个问题

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430141310532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
和这个urllib.error.URLError: &lt;urlopen error [SSL: WRONG_VERSION_NUMBER] wrong version number (_ssl.c:1045)&gt;

结论：看来这可能不是dns,而是被屏蔽了，后两个问题并不是问题，只是屏蔽和网络延迟导致的问题

现在成功了

[1] https://blog.csdn.net/jiangyunsheng147/article/details/79420515?
ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158822468019724846460925%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.57662%2522%257D&amp;request_id=158822468019724846460925&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog
2<sub>all</sub>first_rank_v2~rank_v25-2
