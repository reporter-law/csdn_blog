# 原创

： with open() 出现FileNotFoundError: [Errno 2] No such file or directory

# with open() 出现FileNotFoundError: [Errno 2] No such file or directory

@[TOC](with open() 出现FileNotFoundError: [Errno 2] No such file or directory)

# 一、报错<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20201024175216822.jpg#pic_center"/>

```
with open(output + "doc_to_docx_succuse.txt", "r", encoding="utf-8")as f1:
FileNotFoundError: [Errno 2] No such file or directory: 'E:\\Firefox\\docxdoc_to_docx_succuse.txt'

```

# 二、解决

with open() as f<br/> 用来打开本地文件的，使用完毕后，自动关闭文件，无需手动书写close(),同时文件不存在时会自动创建一个文件

因而照理说不应该出现

```
	FileNotFoundError: [Errno 2] No such file or directory

```

解决方法将

```
"r"改为"a+"
即
with open(output + "xxx.txt", "a+", encoding="utf-8")as f:
	f.read()

```

为什么可以解决的原理暂不明
