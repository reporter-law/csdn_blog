# 原创

： plotly动态可视化：理解关键在于数据的结构 ：

原力计划

# plotly动态可视化：理解关键在于数据的结构

### plotly动态可视化：理解关键在于数据的结构

# 一、问题

源码：这应该是官网上的一个示例，不过我不是在官网上看到的，而是在其他地方看到的<br/> import plotly.express as px<br/> ‘’‘气泡动态图’’’

```
df = px.data.gapminder()#预设数据
fig = px.scatter(df, x="gdpPercap", y="lifeExp", animation_frame="year", 	animation_group="country",
       size="pop", color="continent", hover_name="country",
       log_x=True, size_max=55, range_x=[100,100000], range_y=[25,90])

#fig["layout"].pop("updatemenus") # optional, drop animation buttons
fig.show()

```

有了这个源码后，首先找到

```
df = px.data.gapminder()

```

这是一个数据，数据不在本地，而是需要通过网络进行数据请求，内部似乎有一个request,当导入时就会自动request相应数据<br/>
数据内容为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052522494153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
其格式为&lt;class ‘pandas.core.frame.DataFrame’&gt;<br/> 是pandas的dataframe

因此照葫芦画瓢，随意在excel中建立了一个test格式数据，用pandas读取

```
path = 'J:\PyCharm项目\项目\项目二_文书内容提取\输出模块\word_data.xlsx'
data_frame = pd.read_excel(path,index_col=None)
print(type(data_frame))
print(data_frame)

```

&lt;class ‘pandas.core.frame.DataFrame’&gt;<br/> 格式一致

```
import pandas as pd
import plotly.express as px


path = 'J:\PyCharm项目\项目\项目二_文书内容提取\输出模块\word_data.xlsx'
data_frame = pd.read_excel(path,index_col=None)
print(type(data_frame))
print(data_frame)

fig =px.bar(data_frame, x="频率",y='分词', animation_frame="year", 
        orientation = 'h',range_x=[0, data_frame.频率.max()],color = '分词'

       )

```

原本数据只有两列，索引和值，但是动态效果需要animation_frame，就随便弄了个年份，

年份内容为行值（请注意问题就在这里，后面会说到）！！！！！

格式为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525225946656.png"/>

结果输出了这样的内容<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052523011387.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

动态也能动，但是就是特别难道，只有一个数据，和上面示例的完全不一样<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525230346801.gif"/>

太难看了，占据了整个版面

# 二、解决路径

## 一、参数

我一直以为是参数的原因，即是不是某个参数我没有加上，导致图片仅显示一个条块，而不是有很多条形一起动

结果这几天找遍了相关文章，也看来官方文档，始终没有找到这个参数<br/>
找到一个比较有用的参数中文解释文章《可视化神器Plotly_Express详解》，链接: [link](https://www.360kuai.com/pc/9ceb94c49b5a9920f?cota=4&amp;kuai_so=1&amp;tj_url=so_rec&amp;sign=360_57c3bbd1&amp;refer_scene=so_1).<br/>
但是在参数以及api方法寻找中，发现其实图形可以叠加，例如《python绘制折线图（多条）》，链接: [link](https://blog.csdn.net/super_he_pi/article/details/85987543?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-7.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-7.nonecase).<br/>
多条折线图，需要构造多个绘图方法

因而我想是不是需要多次绘图即将

```
fig =px.bar(data_frame, x="频率",y='分词', animation_frame="year", 
        orientation = 'h',range_x=[0, data_frame.频率.max()],color = '分词'

       )
fig_ =px.bar(data_frame, x="频率",y='分词', animation_frame="year", 
        orientation = 'h',range_x=[0, data_frame.频率.max()],color = '分词'

       )
data=[fig,fig_]
figs=go.Figure(data=data, layout=layout)
figs.show()

```

变成这样两个方法，然后通过go.Figure(）将之组合起来,但是仍然不行

## 二、数据格式

今天突然发现是数据格式问题，year和分词的数量上需要相当，也即数据需要是类型化的，是几类数据的合并数据集<br/>
如：test2<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525232114633.png"/>

这样导入后才能形成多个条形图，因为如上所示其实就是几类数据的合并展示，将每一类数据作为一个条形

之后：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200525232250921.gif"/>
