# 原创

： 《python数据分析基础》4.1.1：报错——sqlite3.OperationalError: table csv has 5 columns but 4 values were supplied

# 《python数据分析基础》4.1.1：报错——sqlite3.OperationalError: table csv has 5 columns but 4 values were supplied

第一个报错：sqlite3.OperationalError: table csv has 5 columns but 4 values were supplied

原因：没有使用与作者一致的csv数据内容<br/>
我的csv文件内容为4.1中的数据内容，进行了重复而已<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428173400341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这个csv与作者的csv不同之处在于只有四列，作者有五列，但是在

```
table = """CREATE TABLE IF NOT EXISTS csv
        (csv_name VARCHAR(20),
        customer VARCHAR(20),
        product VARCHAR(40),
        amount FLOAT,
        date DATE);
        """

```

一开始没有进行数据拉伸，所以刚好行也是五行，认为在表头添加了就可以的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428173625898.png"/><br/>
但是（读取方式不是行而是列读取）<br/> 所以一共只有四列，此处csv_name VARCHAR(20),需要去掉即

```
table = """CREATE TABLE IF NOT EXISTS csv
        (
        customer VARCHAR(20),
        product VARCHAR(40),
        amount FLOAT,
        date DATE);
        """

```

但是这里比较坑的地方在于，即使出错，生成的sqlite.db也会生成，于是再次运行时就会继续报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428174001126.png"/><br/>
需要删除进行在运行才可以，否则一直出现这个报错。

第二个报错<br/> sqlite3.ProgrammingError: Incorrect number of bindings supplied. The current statement uses 5, and there are
4 supplied.

原因：没有使用与作者一致的csv数据内容<br/> 我的csv文件内容为4.1中的数据内容，进行了重复而已

这个主要在于插入数据占位的“？”处多给了一个“？”

```
for row in file_reader:
data=[]
for column_index in range(len(header)):
    data.append(row[column_index])
print(data)
statement = 'INSERT INTO csv VALUES(?,?,?,?,?);'

```

也是由于我的只有四列数据，但是占位5个位置导致的报错

修改之后成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428174540181.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428174605950.png"/><br/>
不按照书上的来有好处也有坏处，<br/> 好处就是需要自己解决问题、看报错内容<br/> 坏处就是学习进度慢
