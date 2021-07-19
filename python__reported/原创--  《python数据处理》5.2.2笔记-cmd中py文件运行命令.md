# 原创

： 《python数据处理》5.2.2笔记：cmd中py文件运行命令

# 《python数据处理》5.2.2笔记：cmd中py文件运行命令

### 《python数据处理》5.2.2笔记：cmd中py文件运行命令

# 一、问题

在cmd中直接运行书中的源码：

注：修改了范例<br/> pdf2txt.py -o I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.txt I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.pdf

会出现pd2txt.py文件即：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051207585946.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
然而txt的内容就没有<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200512075931749.png"/>

# 二、解决思路

1、可能是环境问题？

```
os.system('pdf2txt.py -o I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.txt   I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.pdf')

```

但是效果一样

2、可能是python解释器没有运行，在前面增加命令

```
python -m pdf2txt.py -o I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱 学强.txt I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.pdf

```

报错：

```
D:\Users\Administrator\AppData\Local\Programs\Python\Python37\python.exe: Error while finding module specification for 'pdf2txt.py' (ModuleNotFoundError: No module named 'pdf2txt')

```

可能是命令出错，因为运行的是py文件不是module

3、更改命令

```
	python pdf2txt.py -o I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.txt I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.pdf

```

报错：

```
(null): can't open file 'pdf2txt.py': [Errno 2] No such file or directory

```

文件没有找到，这可能是由于系统重装后，python解释器没有在C盘，那就明确路径

```
python D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\pdf2txt.py  -o I:\桌面文件\捕诉模式\恢复重建以来检察机关内设机构改革的历史经验与启示_邱学强.txt I:\桌面文件\捕诉模式\恢复重建以来检察机关内 设机构改革的历史经验与启示_邱学强.pdf

```

现在成功了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051208094430.png"/>

问题：复制过来的命令无缘无故报错

```
Traceback (most recent call last):
File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\pdf2txt.py", line 115, in &lt;module&gt;
if __name__ == '__main__': sys.exit(main(sys.argv))
	File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\pdf2txt.py", line 104, in main
with open(fname, 'rb') as fp:
FileNotFoundError: [Errno 2] No such file or directory: 'I:\\桌面文件\\捕诉模式\\恢复重建以来检察机关内'

```

但是重新输一遍又好了。
