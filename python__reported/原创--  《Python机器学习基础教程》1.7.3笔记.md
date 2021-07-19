# 原创

： 《Python机器学习基础教程》1.7.3笔记

# 《Python机器学习基础教程》1.7.3笔记

### 《Python机器学习基础教程》1.7.3笔记

# 第一个报错：AttributeError: module ‘pandas’ has no attribute ‘scatter_matrix’

报错内容：

```
AttributeError: module 'pandas' has no attribute 'scatter_matrix'

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200616163550434.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
原因：pandas版本更改<br/> 需要在前面增加plotting.即

```
grr = pd.plotting.scatter_matrix(iris_dataframe, c=y_train, figsize=(15, 15),
                       marker='o', hist_kwds={'bins': 20}, s=60,
                       alpha=.8, cmap=mglearn.cm3)

```

这个报错在源码中已经修改过来了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202006161639106.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 第二个报错：MatplotlibDeprecationWarning: The colNum attribute was deprecated in Matplotlib 3.2 and will be removed two minor relea

报错内容:

```
MatplotlibDeprecationWarning:  The colNum attribute was deprecated in Matplotlib 3.2 and will be removed two minor relea.....

```

原因：matlplotlib版本更改<br/>
方法：卸载最新版本，换成之前的版本，我换成了2.2.5<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020061616403140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 第三个问题：没有图形显示

在pycharm中换成旧版本仍然无法输出，但是也没有报错。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200616164207715.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

原因：如同matplotlib绘图一样需要进行展示，即plt.show()

方法：增加show()的命令

```
import matplotlib.pyplot as plt
grr = pd.plotting.scatter_matrix(iris_dataframe, c=y_train, figsize=(15, 15),
                       marker='o', hist_kwds={'bins': 20}, s=60,
                       alpha=.8, cmap=mglearn.cm3)
plt.show()

```

展示成果<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200616164400801.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
