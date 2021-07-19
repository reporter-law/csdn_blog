# 原创

： 《Python机器学习基础教程》第一章笔记（最简单的监督学习）：鸢尾花品种预测

# 《Python机器学习基础教程》第一章笔记（最简单的监督学习）：鸢尾花品种预测

### 《Python机器学习基础教程》第一章笔记（最简单的监督学习）：鸢尾花品种预测

# 三行程序

```
from sklearn.datasets import load_iris
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier	

iris_dataset = load_iris()
X_train,X_test,y_train,y_test = train_test_split(iris_dataset['data'],iris_dataset['target'],random_state=0)
knn = KNeighborsClassifier(n_neighbors=1)
knn.fit(X_train,y_train)

```

到此处已经完成了模型的训练！

```
iris_dataset = load_iris()

```

是导入鸢尾花数据集，这个数据集应该是requests过来的

```
X_train,X_test,y_train,y_test = train_test_split(iris_dataset['data'],iris_dataset['target'],random_state=0)

```

这是对于数据集进行拆分，75%划分为训练集，25%划分为预测集<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200616172456826.png"/><br/>
其中两个元素的是x,一个元素的是y,(112,4)的意思是114个样本，4是指四个数据即鸢尾花的花萼长宽、花瓣的长宽

```
knn = KNeighborsClassifier(n_neighbors=1)

```

是在实例化k近邻算法，k近邻算法就是一个监督学习的算法

```
knn.fit(X_train,y_train)

```

将训练集丢入算法中训练出来相关模型

以下为一个预测：<br/> X_new = np.array([[5,2.9,2,0.2]])<br/> prediction = knn.predict(X_new)<br/> print(prediction)
#标签转为数据的输出<br/> print(iris_dataset[‘target_names’][prediction])<br/>
这是输出的预测内容，鸢尾花的品种为：‘setosa’<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200616172953174.png"/>

虽然预测成功了，但是预测是否准确呢？此时需要用到测试集，通过对比预测值与测试集中的实际值可以确认其预测准确度，使用score方法

```
print('预测精度为： {:.2f}'.format(knn.score(X_test,y_test)))

```

预测精确度为：
