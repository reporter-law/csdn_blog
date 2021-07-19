# 原创

： 《python数据分析基础》ggplot：AttributeError: module 'pandas' has no attribute 'tslib'

# 《python数据分析基础》ggplot：AttributeError: module 'pandas' has no attribute 'tslib'

在《python数据分析基础》6.3ggplot使用过程中报错

```
from ggplot import *
print(diamonds.head())

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430095225642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
按照报错打开<br/>
注意：修改时修改ggplot的函数或者方法名称，而不要修改pandas的函数或者方法名。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430095306246.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430095327291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
date_types = (
pd.tslib.Timestamp,
pd.DatetimeIndex,
pd.Period,
pd.PeriodIndex,
datetime.datetime,
datetime.time)

```

tslib在pandas中 别名_tslib<br/> 将之改为_tslib后，继续报错ModuleNotFoundError: No module named
‘pandas.lib’<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430095648204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

按照上步骤继续修改

```
from pandas.lib import Timestamp
#修改为
from pandas._libs import Timestamp

```

继续报错：AttributeError: module ‘pandas’ has no attribute
‘tslib’<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430095913611.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
继续修改：

```
date_types = (
pd.tslib.Timestamp,
pd.DatetimeIndex,
pd.Period,
pd.PeriodIndex,
datetime.datetime,
datetime.time)
#修改为
date_types = (
pd._tslib.Timestamp,
pd.DatetimeIndex,
pd.Period,
pd.PeriodIndex,
datetime.datetime,
datetime.time)

```

三次修改后成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430100052771.png"/>

原因：可能是版本问题，即pandas最新版与ggplot之间存在版本差距，即ggplot引用的是旧版的pandas.<br/>
ggplot的最新版也是2016年的呢，一直没有更新<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020043010034468.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

但是，我的pandass是1.0.1的新版<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430100541910.png"/><br/>
而pandas1.0.1发行时间为2020年<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430100653151.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
所以函数名称存在变化，因而修改时修改ggplot更好，修改pandas会影响其他mudule的使用。

```
from ggplot import *
print(diamonds.head())
plt3 = ggplot(diamonds, aes(x='carat', y='price', color='cut')) + 	geom_point(alpha=0.5) + \
    scale_color_gradient(low='#05D9F6', high='#5011D1') + xlim(0,6) + ylim(0,20000) + \
    xlab('Carat') +ylab('Price') + ggtitle('Diamond Price By Carat and Cut') + theme_gray()
print(plt3)
ggplot.save(plt3,"ggplot_plots.png")
#此处的源码为ggsave(plt3,"ggplot_plots.png"),
#应当修改为ggplot.save(plt3,"ggplot_plots.png")

```

不然会报错：NameError: name ‘ggsave’ is not
defined<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430102422580.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
最后画出来的图形为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200430102511340.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
