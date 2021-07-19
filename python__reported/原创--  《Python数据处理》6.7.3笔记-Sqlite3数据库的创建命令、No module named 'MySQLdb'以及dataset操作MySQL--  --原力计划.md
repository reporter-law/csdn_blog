# 原创

： 《Python数据处理》6.7.3笔记:Sqlite3数据库的创建命令、No module named 'MySQLdb'以及dataset操作MySQL ：

原力计划

# 《Python数据处理》6.7.3笔记:Sqlite3数据库的创建命令、No module named 'MySQLdb'以及dataset操作MySQL

### 《python数据处理》6.7.3笔记:sqlite3数据库的创建命令

# 一、创建不成功的源码

源码：

```
sqlite3 data_wrangling.db

```

报错：

```
'sqlite3' 不是内部或外部命令，也不是可运行的程序或批处理文件。

```

# 二、成功创建的代码

源自《python数据分析基础》

```
import sqlite3

con = sqlite3.connect('data_wrangling.db')
con.commit()

```

# 三、dataset链接mysql

示例代码，源自dataset示例，链接: [link](https://dataset.readthedocs.io/en/latest/quickstart.html#reading-data-from-tables).

```
# connecting to a MySQL database with user and password
db = dataset.connect('mysql://user:password@localhost/mydatabase')
table = db['user']
table.insert(dict(name='John Doe', age=46, country='China'))
 print(db.tables)

```

## 第一个报错：

```
ModuleNotFoundError: No module named 'MySQLdb'

```

缺少MySQLdb，参照《MySQLdb安装与使用》，下载MySQL-Python,<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512141727766.png"/>

## 第二个报错：

```
error: Microsoft Visual C++ 14.0 is required. Get it with "Build Tools for Visual Studio": https://visualstudio.microsoft.com/downloads/

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512141640675.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
还要下载 Microsoft Visual C++ 14.0，

参照《解决error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools"
两个方法》找到办法，但是在检索Microsoft Visual C++ 14.0时发现Microsoft Visual C++ 14.0就是Visual Studio Community 2019的旧版啊！

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512141933110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是已经下载了Visual Studio Community
2019<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512141625351.png"/><br/> 不应该有问题的啊!

重新找了一篇文章《Python创建本地数据库》，MySQLdb在mysqlclient中，于是

```
import os

os.system('pip install -i https://pypi.tuna.tsinghua.edu.cn/simple mysqlclient')

```

下载成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512142304118.png"/>

重新connect mysql没有报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512142424976.png"/>

## 第三个报错：

```
sqlalchemy.exc.OperationalError: (MySQLdb._exceptions.OperationalError) (2002, "Can't connect to MySQL server on 'localhost' (10061)")

```

一看没有启动mysql,那就启动

## 第四个报错：

```
sqlalchemy.exc.OperationalError: (MySQLdb._exceptions.OperationalError) (1049, "Unknown database 'mydatabase'")

```

原因：没有创建数据库

创建数据库mydatabase的指令

```
import pymysql

db = pymysql.connect(host = 'localhost', user = 'root', password = '你自己的密码', port = 3306)
cursor = db.cursor()
cursor.execute("CREATE DATABASE mydatabase DEFAULT CHARACTER SET utf8")
db.close()

```

使用pymysql创建的数据库mydatabase

现在成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512143840766.png"/>

使用dataset也可以创建

对源码进行改进

源码：

```
	result = db.query('SELECT country, COUNT(*) c FROM user GROUP BY country')
for row in result:
	print(row['country'], row['c'])

```

利用query（）进行mysql传参

```
db = dataset.connect('mysql://root:（密码）@localhost')
result = db.query("CREATE DATABASE mydatabase_ DEFAULT 	CHARACTER SET utf8")
db = dataset.connect('mysql://root:密码@localhost/mydatabase_')
table = db['users']
table.insert(dict(name='John Doe', age=46, country='China'))
print(db.tables)

```
