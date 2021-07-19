# 原创

： 《Python数据处理》9.1.1导入数据笔记：agate.exceptions.CastError: Can not parse value as Decimal. Error at row ：

原力计划

# 《Python数据处理》9.1.1导入数据笔记：agate.exceptions.CastError: Can not parse value as Decimal. Error at row

### 《Python数据处理》9.1.1导入数据笔记：agate.exceptions.CastError: Can not parse value as Decimal. Error at row

成功去掉报错后的截图<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516103338188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 一、报错现象：

源码：

```
def agate_data_check(self):
    '''数据类型猜测,将xlrd数据类型转为agate数据类型'''
    text_type = agate.Text()
    number_type = agate.Number()
    boolean_type = agate.Boolean()
    date_type = agate.DataType()

    example_row = self.xlrd_read_xls().row(6)
    #示例
    print(example_row)
    print(example_row[0].ctype)#类型
    print(example_row[0].value)
    print(ctype_text)#这应当是一个固定的设置的字典
    '''xlrd的数据类型'''

    '''将xlrd的数据类型转为agate的数据类型'''
    types = []
    for v in example_row:
        '''ctype_text为字典'''
        value_type = ctype_text[v.ctype]
        #一个一个
        #print(value_type, end=' ')
        if value_type == 'text':
            types.append(text_type)
        elif value_type == 'number':
            types.append(number_type)
        elif value_type =='xldate':
            types.append(date_type)
        else:
            types.append(text_type)
    for type in types:
        pass
    #return types
        #pprint.pprint(type)
    '''导入agate表中'''
    table = agate.Table(self.country_data(), self.combine_title(), types)#self.agate_data_check())

```

在此处进了函数封装，基本内容与书上源码一致，或许存在变量名有不一致的地方

运行后出现报错

```
agate.exceptions.CastError: Can not parse value "" as Decimal. Error at row 1 column Place of residence (%) Urban.

```

而没有出现书中所述的

```
CastError can not convert value '-' to Decimal for NumberColumn

```

即使进行清理

```
 def get_new_array(self, clean_function):
    new_arr = []
    for row in self.country_data():
        clean_row = [clean_function(rv) for rv in row]
        new_arr.append(clean_row)
    pprint.pprint(new_arr)
    table = agate.Table(new_arr, self.combine_title(), self.agate_data_check()
    #注：同上进行过封装，所以titles变成了self.combine_title()

```

一样的报错

# 二、解决方法

由于与书中错误不同，所以自行解决问题

## 第一步：

最后一个报错为

```
agate.exceptions.CastError: Can not parse value "" as Decimal. Error at row 1 column Place of residence (%) Urban.

```

位于

```
File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\agate\table\__init__.py", line 133, in __init__
raise CastError(str(e) + ' Error at row %s column %s.' % (i, self._column_names[j]))

```

找到这个文件，将except内容注释掉<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/202005161022253.png"/><br/> 结果成功

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516102452660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516102509467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

注意：如果第一步未成功则进行第二步：

## 第二步：

首先，<br/> (ps:在第一次如同第一步修改时，出现一样的报错即修改未成功，但是第二次只进行第一步时的修改时成功了，可能会需要先进行第二步）

```
agate.exceptions.CastError: Can not parse value "" as Decimal. Error at row

```

然后向上看上一个报错：

```
agate.exceptions.CastError: Can not parse value "" as Decimal.

```

位于<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516102641969.png"/><br/>
注释掉<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516102720588.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
结果contries and
area为空。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051610274688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

其次，去掉注释进行还原

最后，回到第一步的修改方式

运行结果<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200516103338188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、疑惑

不知道为什么，其修改后成功的原理不明
