# 原创

： 《Python机器学习基础教程》第二章笔记:ValueError: cannot reshape array of size 4000000 into shape (1000,1000)

# 《Python机器学习基础教程》第二章笔记:ValueError: cannot reshape array of size 4000000 into shape (1000,1000)

@[TOC](《Python机器学习基础教程》第二章笔记:ValueError: cannot reshape array of size 4000000 into shape (1000,1000))

成功解决：<br/> 增加命令

```
y = y % 2

```

# 一、报错

```
ValueError: cannot reshape array of size 4000000 into shape (1000,1000)

```

# 二、尝试解决

意思：ValueError：无法将大小为4000000的数组重塑为形状（1000,1000）<br/> 数组没有办法重塑

尝试解决的思路：<br/> 1、查看源码：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200620103540418.png"/><br/>
没有看懂！!!!<br/> 不过没有关系

2、其中centers为控制y中值类别的参数<br/> 默认为2

此时赋值为4

3、输出一下y<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200620103807621.png"/><br/>
对比没有赋值为4是：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200620103952317.png"/><br/> 即此时为3

将centers赋值为2 时，成功输出

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200620104104629.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200620104113190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

由此可见，需要对center或者y进行调整，由于需要center=4，因而调整y,使得y=y%2即可

```
X, y = make_blobs(centers=4,random_state=8)#centers为数据堆
print(y)##centers为数据堆改变了y的值
y = y % 2
print(y)
linear_svm = LinearSVC().fit(X, y)
mglearn.plots.plot_2d_separator(linear_svm, X)#classification可以
mglearn.discrete_scatter(X[:, 0], X[:, 1], y)
plt.xlabel("Feature 0")
plt.ylabel("Feature 1")
plt.show()

```

参考<br/> [1]小书同学:《监督学习(九)——核支持向量机SVM》，链接: [link](https://www.jianshu.com/p/c2416594e8ba).
