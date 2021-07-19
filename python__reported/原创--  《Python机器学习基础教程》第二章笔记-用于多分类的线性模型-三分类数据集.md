# 原创

： 《Python机器学习基础教程》第二章笔记：用于多分类的线性模型-三分类数据集

# 《Python机器学习基础教程》第二章笔记：用于多分类的线性模型-三分类数据集

### 《Python机器学习基础教程》第二章笔记：用于多分类的线性模型-三分类数据集

# 一、疑问

第一个数据集的可视化：

```
from sklearn.linear_model import LogisticRegression
from sklearn.svm import LinearSVC
import mglearn
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split

X, y = mglearn.datasets.make_forge()
print(y)

fig, axes = plt.subplots(1, 2, figsize=(10, 3))

for model, ax in zip([LinearSVC(), LogisticRegression()], axes):
clf = model.fit(X, y)

mglearn.plots.plot_2d_separator(clf, X, fill=False, eps=0.5,
                                ax=ax, alpha=.7)#画线的命令
mglearn.discrete_scatter(X[:, 0], X[:, 1], y, ax=ax)#画点的命令
ax.set_title(clf.__class__.__name__)
ax.set_xlabel("Feature 0")
ax.set_ylabel("Feature 1")
axes[0].legend()
plt.show()	

```

其实就是45页的图2-15的Logistic回归<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020061821390187.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

第二个数据集的可视化：

```
from sklearn.datasets import make_blobs
import mglearn
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.svm import LinearSVC


X, y = make_blobs(random_state=42)#random_state=42报持随机一致

mglearn.discrete_scatter(X[:, 0], X[:, 1], y)
#plt.scatter(X[:, 0], X[:, 1], y)#这也是两个数据集
plt.xlabel("Feature 0")
plt.ylabel("Feature 1")
plt.legend(["Class 0", "Class 1", "Class 2"])
plt.show()

```

就是50页图2-19：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618214053146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

问题：

```
都是：mglearn.discrete_scatter(X[:, 0], X[:, 1], y)

```

问什么一个是两类一个是三类

为此还专门对第二个数据集利用matplotlib进行可视化，发现确实是两个数据，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618214241421.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

应该一样啊！为什么第二个数据集会有三类

# 二、理解

命令行中X为二维数据集因而[:, 0]第一列# 输入X第0列和第1列作为x轴,将y作为y轴，纯数据上来说是应该与matplotlib进行可视化一样只有两类，

但是mglearn绘图并不是xy绘图，即y不是x的值，y就是类别本身

第一个数据集只有两类是因为y值只有0、1<br/> 例如第一个数据集的y<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618214634801.png"/>

第二个数据集的y<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618214722198.png"/>

这个0、1、2就像鸢尾花数据集中的[‘target’]一样只是一个类别代数
