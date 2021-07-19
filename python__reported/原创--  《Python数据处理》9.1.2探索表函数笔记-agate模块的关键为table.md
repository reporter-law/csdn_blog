# 原创

： 《Python数据处理》9.1.2探索表函数笔记：agate模块的关键为table

# 《Python数据处理》9.1.2探索表函数笔记：agate模块的关键为table

### 《Python数据处理》9.1.1导入数据笔记

# 一、问题

## 问题一：

源码：

```
most_egregious = table.order_by('Total (%)', reverse=True).limit(10)

```

报错：

```
KeyError: 'Total (%)'

```

可能是自己写错了，但是agate出来的也是<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051612040522.png"/><br/>
没有找出来哪里错了<br/> 只能修改为

```
most_egregious = table.order_by(table.column_names[1], reverse=True).limit(10)

```

## 问题二：

整体比较混乱：<br/> cpi_types = get_types(cpi_sheet.row(3))<br/> 位于<br/> get_types(cpi_sheet.row(3))导致阅读具有一定障碍<br/>
这一节感觉整体阅读具有障碍，变量太多而没有罗列清楚，<br/> 且

```
cpi_rows = get_new_array(cpi_rows,float_to_str)

```

中的float_to_str一直没有找到

加上之前试图封装9.1.1、9.1.2的内容导致函数调用非常麻烦，整整折腾了一下午和一个晚上

错误示例：

```
from 数据导入 import Data_explore
import xlrd
import agate
from 探索表函数 import Data_Sort
#两个中文就是前两个封装的内容

def xlrd_cpi():
	tm = Data_explore('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls')
#print(tm.path)
 	tm.xls_type()
	print(tm.agate_data_check())
	table = tm.get_new_array()
#print(table.column_names)


xlrd_cpi()
def table_():
	tm = Data_explore('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls')
	table = tm.get_new_array()
	print(table.column_names)
#table_()

def get_table():
try:
    tm = Data_explore('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls')
    table = tm.get_new_array()
    print(table)
    '''DuplicateColumnWarning: Column name "1.0 3.0" already exists in Table. Column will be renamed to "1.0 3.0_2".'''
except Exception as e:
    print(e)
#get_table()
def repeat_row_manage():

	 tm = Data_explore('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls')
	index = 0
	title_ = [titles + ' '  for titles in tm.combine_title() if titles]
	#print(type(title))
	tm_ =Data_explore('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls',title_)
	#print(tm_.title)




	#print(title)
	#print(tm.combine_title())#tm.combine_title是一个列表
	print()
	table = tm_.get_new_array()#错误原因没有变成tm_
	#print(table)
	t = Data_Sort()
	ranked = t.data_table_rank()
	cpi_and_cl = table.join(ranked, table.column_names[1], ' Countries and areas', inner=True)

	print(cpi_and_cl.column_names)

	for r in cpi_and_cl.order_by('CPI 2013 Score').limit(10).rows:
    	print('{}: {} - {}%'.format(r[tm_.get_new_array.column_names[1]], r['CPI 2013 Score'], r['Total (%)']))
    print('是否运行至此测试------------------------------------------')
#repeat_row_manage()

```

理解的关键：<br/> table需要rows ,title,type.table是agate的基础，table就是xlrd的标题与数据的联合，就是将xlrd内容转换成为agate的内容，而type是需要设置的内容

正常的源码：

```
import xlrd
from xlrd.sheet import ctype_text
import agate
import pprint

from 探索表函数 import Data_Sort


'''table需要rows ,title,type.其中rows'''

def xlrd_open():
	cpi_workbook = xlrd.open_workbook('I:\\360下载\\data-wrangling\\data\\chp9\\corruption_perception_index.xls')
	cpi_sheet = cpi_workbook.sheets()[0]
	return cpi_sheet

def cpi_titles():
	'''簿-表-标题行(行值不是列值）'''
	cpi_sheet = xlrd_open()
	cpi_title_rows = zip(cpi_sheet.row_values(1), cpi_sheet.row_values(2))
	#print(cpi_sheet.row_values(2))
	'''之前测试失败是由于title的拼凑位置不一样，修改会导致原title出错'''
	cpi_titles = [list(t)[0] + ' ' + list(t)[1] for t in cpi_title_rows]
 	#print(cpi_titles)
	cpi_titles = [t.strip() for t in cpi_titles]
	#print(cpi_titles)
	return cpi_titles
print(cpi_titles())


#def cpi_rows():
'''行数的值，正式行数的值'''
cpi_sheet = xlrd_open()
cpi_rows = [cpi_sheet.row_values(r) for r in range(3, cpi_sheet.nrows)]
#与数据导入中的有效行也不一致
#print(cpi_rows)#是正式的数据行，没有表头
'''函数化后无法输出，只能输出内存地址'''



def cpi_types():
 '''行类型，对正式数据行的行类型'''
	cpi_sheet = xlrd_open()
	types = []
	text_type = agate.Text()
	number_type = agate.Number()
	boolean_type = agate.Boolean()
	date_type = agate.DataType()
	for v in cpi_sheet.row(3):
    	'''ctype_text为字典'''
    	value_type = ctype_text[v.ctype]
    	
    	# print(value_type, end=' ')
    	if value_type == 'text':
            types.append(text_type)
    	elif value_type == 'number':
        	types.append(number_type)
    	elif value_type == 'xldate':
        	types.append(date_type)
    	else:
        	types.append(text_type)
	return types


def cpi_titles_update():
	global cpi_titles
	cpi_titles = cpi_titles()
	cpi_titles[0] = cpi_titles[0] +'Duplicate'
	return cpi_titles
'''针对更新后的title进行table输出'''
cpi_table = agate.Table(cpi_rows,cpi_titles_update(),cpi_types())
cpi_table.print_table(max_columns=7)






'''数据集连接'''
	
ranked = Data_Sort().data_table_rank()#.print_table(max_columns=7)
cpi_and_cl = cpi_table.join(ranked, 'Country / Territory', ' Countries and areas', inner=True)
print(cpi_and_cl.column_names)
for r in cpi_and_cl.order_by('CPI 2013 Score').limit(10).rows:
	print('{}: {} - {}%'.format(r['Country / Territory'], r['CPI 2013 Score'], r['Total (%) ']))

```
