# 原创

： pandas依据多列数据生成某一列数据-兼pandas数据修改汇总

# pandas依据多列数据生成某一列数据-兼pandas数据修改汇总

### pandas依据多列数据生成某一列数据

# 一、数据修改

网上pandas的数据修改大多是依据某一列数据进行修改或者生成了，几乎没有找到依据多列数据生成或者修改某一列的

依据某一列数据修改某一列数据的方法：<br/> 方法一：

```
df.loc[df.a&gt;=2,'b'] = 'new_data'

```

来自chenpe32cp：《python
pandas如何基于某一列修改某一列的值》，链接: [python pandas如何基于某一列修改某一列的值](https://blog.csdn.net/chenpe32cp/article/details/82180537?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=pandas%E5%88%97%E6%95%B0%E6%8D%AE%E6%9B%B4%E6%96%B0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~sobaiduweb~default-1-82180537)
.

方法二：

```
df["a"]=df["b"].map(lambda x: x+1)

```

来自Allan-li：《对DataFrame中某一列数据进行修改的方法》，接: [对DataFrame中某一列数据进行修改的方法](https://blog.csdn.net/li_0891/article/details/81020657?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.nonecase)
.

# 二、依据多列数据修改某一列

此处目标为依据“比例”和“选定法定刑”生成“幅度法定刑”<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200713101548188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200713101602790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

之前主要是对某一列修改，运用的是方法二，因而此处的依据多列数据修改某一列是再次基础上的更进一步，通过循环来完成

```
 for a,b in zip(df["比例"],df["选定法定刑"]):
    element.append(drm(a,b))
df["幅度法定刑"] = element

```

其中的drm()是预先设定的一个函数<br/> 完整的为：

```
def data_random_margin(x,y):
	 list_math = [i for i in range(int(y),181)]
	#print(list_math)
	 len_ = len(list_math)
if int(len_)&gt;2:
    if x &lt; 0.10547166487854089:
        wieght = np.random.randint(1, 2, len_)
        list_math_split_1 = wieght[:int(len_ / 2)]
        list_math_copy_1 = []
        list_math_split_2 = wieght[int(len_ / 2):]
        list_math_copy_2 = []
        for i, content in enumerate(list_math_split_1):
            content = content - x / 7500 * i
            list_math_copy_1.append(content)
        # print(list_math_copy_1)
        for i, content in enumerate(list_math_split_2):
            content = content + x / 7500 * i
            list_math_copy_2.append(content)

        wieght_ = list_math_copy_1 + list_math_copy_2
        # print(wieght_)

        data = random.choices(list_math, weights=wieght_)
        return data[0]

    elif x == 0.10547166487854089:
        wieght = np.random.randint(1, 2, 151)
        data = random.choices(list_math, weights=wieght)
        return data[0]
    elif x &gt; 0.10547166487854089:

        wieght = np.random.randint(1, 2, len_)
        list_math_split_1 = wieght[:int(len_ / 2)]
        list_math_copy_1 = []
        list_math_split_2 = wieght[int(len_ / 2):]
        list_math_copy_2 = []
        for i, content in enumerate(list_math_split_1):
            content = content + x / 7500 * i
            list_math_copy_1.append(content)

        for i, content in enumerate(list_math_split_2):
            content = content - x / 7500 * i
            list_math_copy_2.append(content)
        list_math_copy_1 = sorted(list_math_copy_1, reverse=True)
        wieght_ = list_math_copy_1 + list_math_copy_2
        # print(wieght_)

        data = random.choices(list_math, weights=wieght_)
        return data[0]
	


from 项目.中国裁判文书网.selenium路线.数据集处理过程.中文年份数字化 import data_random_margin as drm
 for a,b in zip(df["比例"],df["选定法定刑"]):
    element.append(drm(a,b))
df["幅度法定刑"] = element

```

不太好的一点就是速度特别慢，
