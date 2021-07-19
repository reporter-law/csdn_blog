# 原创

： 《Python数据处理》9.1.6创建分组笔记：NameError：name text_type is not defined

# 《Python数据处理》9.1.6创建分组笔记：NameError：name text_type is not defined

### 《Python数据处理》9.1.6创建分组笔记：NameError：name text_type is not defined

# 一、现象

```
源码：

import json
from 数据集连接再测试 import cpi_and_cl
import pprint
import agate
path = 'I:\\360下载\\data-wrangling\\data\\chp9\\earth.json'

country_json = json.loads(open(path, 'r', encoding='utf-8').read())

country_dict = {}

for dct in country_json:
'''提取json形成单独对应的组'''
country_dict[dct['name']] = dct['parent']
#pprint.pprint(country_dict)

def get_country(country_row):
 '''获得大洲的名称'''
	return country_dict.get(country_row['Country / Territory'].lower())

```

# pprint.pprint(get_country())

```
#for r in cpi_and_cl().rows:
	#print(r['Country / Territory'],r['continent'])
#continent:大洲
#print(cpi_and_cl().columns[0])
cpi_and_cl = cpi_and_cl().compute([('continent', agate.Formula(text_type, get_country)),])

```

报错：

```
	NameError: name 'text_type' is not defined

```

# 二、解决方法

## (一）查阅文档

链接: [link](https://agate.readthedocs.io/en/1.6.1/cookbook/excel.html?highlight=agate.formula#trim).

但是文档中也是一样<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051721544056.png"/>

## (二）Github中的问题寻找

链接: [link](https://github.com/wireservice/agate/issues/391).<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051721573544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517215804527.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517215925159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
解决方法：

```
full_names = exonerations.compute([
('full_name', agate.Formula(agate.Text(), lambda row: '%(first_name)s %(last_name)s' % row))
])

```

将text_type改为agate.Text()

这样以后就可以了：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200517220136823.png"/>
