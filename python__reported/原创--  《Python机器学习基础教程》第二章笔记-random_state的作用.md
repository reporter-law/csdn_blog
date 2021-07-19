# 原创

： 《Python机器学习基础教程》第二章笔记：random_state的作用

# 《Python机器学习基础教程》第二章笔记：random_state的作用

### 《Python机器学习基础教程》第二章笔记：random_state的作用

# 一、random_state的作用：固定系数与截距

random_state的作用在于固定lr.coef_、lr.intercept_，保证每次模型的系数、截距一致

不加random_state时，系数与截距不停的变化：

```
from sklearn.linear_model import LinearRegression
import mglearn
from sklearn.model_selection import train_test_split
X, y = mglearn.datasets.make_wave(n_samples=60)
X_train, X_test, y_train, y_test = train_test_split(X, y)

lr = LinearRegression().fit(X_train, y_train)
print("lr.coef_:", lr.coef_)
print("lr.intercept_:", lr.intercept_)

```

第一次：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618102908872.png"/><br/>
第二次：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618102933213.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
循环一下会发现每次系数和截距均不一样：

增加random_state后：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020061810331062.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、random_state的取值是对系数排序的结果，random_state值越小，系数越大

第一次取值<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020061810341131.png"/><br/>
系数与截距：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618103433132.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第二次取值<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618103658144.png"/><br/> 系数与截距：

第三次取值：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618103741924.png"/><br/> 系数与截距：

第四次取值：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618103516543.png"/>

系数与截距：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200618103504900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

现象：系数越来越小，截距看不出来规律！！！<br/> 结论：random_state取值越小，系数越大；random_state取值越大，系数越小；两者呈现反比关系
