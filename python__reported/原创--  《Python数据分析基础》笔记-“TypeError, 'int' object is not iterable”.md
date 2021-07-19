# 原创

： 《Python数据分析基础》笔记：“TypeError, 'int' object is not iterable”

# 《Python数据分析基础》笔记：“TypeError, 'int' object is not iterable”

学习《Python数据分析基础》第3章最后一个例子：为每个工作簿和工作表计算总数和均值时，在pandas 实现这个例子中的data
处出现报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200427193309954.png"/><br/> 此处原例子没有添加str()
,但是我运行是出现报错<br/> TypeError, ‘int’ object is not iterable

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200427184743324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
找了半天没有解决，因为此处的

```
	data = {"workbook": os.path.basename(workbook),
            'worksheet': worksheet_name,
            "worksheet_total": total_sales,
            "worksheet_average": average_sales}

```

明显是一个dic格式，而

```
columns=['workbook', 'worksheet', 'worksheet_total', 'worksheet_average']

```

又是一个list格式，根本没有“int”object

但是报错一直过不了，只能一个一个的找，最后发现只有

```
data = {"workbook": os.path.basename(workbook),
        'worksheet': worksheet_name,
        "worksheet_total": total_sales,
        "worksheet_average": average_sales}

```

处的

```
"worksheet_total": str(total_sales),
        "worksheet_average": average_sales)}

```

存在"int"这样的数据结构，因而用str()
强制字符串化<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020042718484697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是str()
后又出现报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200427184910828.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
需要索引，找到了博主August1226的文章《python – 解决If using all scalar values, you must pass an index问题》才解决了这个报错

在后面添加一个index = [0]（ps:注意此处必须是[0]，只是index = 0还是错的）

```
worksheet_data_frames.append(pd.DataFrame(data,
        columns=['workbook', 'worksheet', 'worksheet_total', 'worksheet_average'],index = [0]))

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200427194141982.png"/><br/> 但是即使这样，还是存在excel 文件中格式不正常的

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020042719435364.png"/><br/>
试图使用列表推导式过滤，但是没有成功，筛选掉一些文件后，可以的，但是结果似乎还是不对

等待后续解决！！！！！！！！！！！！！！！！
