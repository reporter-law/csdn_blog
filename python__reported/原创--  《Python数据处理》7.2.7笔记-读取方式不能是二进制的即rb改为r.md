# 原创

： 《Python数据处理》7.2.7笔记：读取方式不能是二进制的即rb改为r

# 《Python数据处理》7.2.7笔记：读取方式不能是二进制的即rb改为r

### 《Python数据处理》7.2.7笔记：读取方式不能是二进制的即rb改为r

# 一、源码有误之处

可能是自己买的盗版的印刷问题，但是更可能是源码错误

源码：

```
from csv import DictReader
import pprint

path = 'I:\\360下载\\data-wrangling\\data\\unicef\\mn.csv'
data = DictReader(open(path, 'rb'))

data_row = [d for d in data]

def combine_data_dict(data_rows):
 	'''合并数据'''
	data_dict = {}
	for row in data_rows:
    key = '%s-%s' % (row.get('HH1'), row.get('HH2'))
    if key in data_dict.keys():
        data_dict[key].append(row)
    else:
        data_dict[key] = [row]
    '''此处作用在于将row中合并的key作为键（如果不存在就设为键）而将row作为key对应的值'''
return data_dict
mn_dict = combine_data_dict(data_row)
print(len(mn_dict))

```

报错

```
Traceback (most recent call last):
File "J:/PyCharm项目/学习进行中/《python数据处理》/基础/数据清洗/数据合并.py", line 12, in &lt;module&gt;
data_row = [d for d in data]
File "J:/PyCharm项目/学习进行中/《python数据处理》/基础/数据清洗/数据合并.py", line 12, in &lt;listcomp&gt;
data_row = [d for d in data]
File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\csv.py", line 111, in __next__
self.fieldnames
File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\csv.py", line 98, in fieldnames
self._fieldnames = next(self.reader)
_csv.Error: iterator should return strings, not bytes (did you open the file in text mode?)

```

翻译为中文：_csv.Error：迭代器应返回字符串，而不是字节（您是否以文本模式打开文件？）

# 二、修改

```
from csv import DictReader
import pprint

path = 'I:\\360下载\\data-wrangling\\data\\unicef\\mn.csv'
data = DictReader(open(path, 'r'))

data_row = [d for d in data]

def combine_data_dict(data_rows):
 	'''合并数据'''
	data_dict = {}
	for row in data_rows:
    key = '%s-%s' % (row.get('HH1'), row.get('HH2'))
    if key in data_dict.keys():
        data_dict[key].append(row)
    else:
        data_dict[key] = [row]
    '''此处作用在于将row中合并的key作为键（如果不存在就设为键）而将row作为key对应的值'''
return data_dict
mn_dict = combine_data_dict(data_row)
print(len(mn_dict))

```

正确输出为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200515090019519.png"/>
