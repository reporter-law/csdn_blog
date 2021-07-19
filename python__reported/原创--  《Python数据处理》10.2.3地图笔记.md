# 原创

： 《Python数据处理》10.2.3地图笔记

# 《Python数据处理》10.2.3地图笔记

### 《Python数据处理》10.2.3地图笔记

# 一、源码问题

源码

```
worldmap_chart = pygal.Worldmap()
worldmap_chart.title = 'Child Labor Worldwide'

cl_dict = {}
for r in ranked.rows:
	cl_dict[r.get('country_code_complete').lower()] = r.get('Total (%)')

worldmap_chart.add('Total Child Labor (%)', cl_dict)
worldmap_chart.render()

```

问题：

```
cl_dict[r.get('country_code_complete').lower()] = r.get('Total (%)')

```

改为

```
cl_dict[r.get('country_code').lower()] = r.get('Total (%)')

```

因为之前该键就是’country_code’

```
worldmap_chart.render_to_png('world_map.png)

```

# 二、render_to_png

```
worldmap_chart.render_to_png('world_map.png')

```

报错：

```
OSError: no library called "cairo" was found
no library called "libcairo-2" was found
cannot load library 'libcairo.so': error 0x7e
cannot load library 'libcairo.2.dylib': error 0x7e
cannot load library 'libcairo-2.dll': error 0x7e

```

似乎是少了包，安装以下包满意没有效果，解决方法参照《pygal输出png问题：dlopen() failed to load a library: cairo /
cairo-2》，链接: [link](https://blog.csdn.net/hacklyc/article/details/77101965).注：未实测<img alt="在这里插入图片描述"
src="https://img-blog.csdnimg.cn/20200518211456523.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
