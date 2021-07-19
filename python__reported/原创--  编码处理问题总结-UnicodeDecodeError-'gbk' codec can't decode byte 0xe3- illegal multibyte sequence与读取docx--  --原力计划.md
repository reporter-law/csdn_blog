# 原创

： 编码处理问题总结：UnicodeDecodeError:'gbk' codec can't decode byte 0xe3: illegal multibyte sequence与读取docx ：

原力计划

# 编码处理问题总结：UnicodeDecodeError:'gbk' codec can't decode byte 0xe3: illegal multibyte sequence与读取docx

在试图打开docx文档内容时，以为可以向读取txt文档一样，于是写下了下面的代码

```
with open('C:\\Users\\Administrator\\Desktop\\案例二.docx','r')as f:
contents = f.read()
print(contents)

```

结果遇上报错：UnicodeDecodeError: ‘gbk’ codec can’t decode byte 0xe3 in position 55: illegal multibyte sequence

解决方法一：<br/> 一看，编码错误，祖传方法encoding='utf-8‘’百试百灵的修改

```
with open('C:\\Users\\Administrator\\Desktop\\案例二.docx','r'，encoding='utf-8‘’)as f:
	contents = f.read()
	print(contents)

```

结果一样报错UnicodeDecodeError: ‘utf-8’ codec can’t decode byte 0x87 in position 10: invalid start
byte<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503142738961.png"/><br/> 我就纳闷了，怎么还有
utf-8都解码不了，utf-8号称‘万国码’’（UTF-8编码：它是一种全国家通过的一种编码，如果网站涉及到多个国家的语言，那么建议选择UTF-8编码。），基本上用上它一切就ok了，怎么还报错。我就打了一个“你好”在里面啊！

但既然是编码错误，就继续。<br/> 之后按照这篇文章《UnicodeDecodeError: ‘gbk’ codec can’t decode byte 0xe9 in position 7581: illegal multibyte
sequence》<br/> 一个一个换编码

```
gbk
gb2312
gb18030
utf-8
utf-16
utf-32
ISO-8859-1

```

都没有效果，<br/> utf-16:UnicodeDecodeError: ‘utf-16-le’ codec can’t decode bytes in position 92-93: illegal
encoding<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503143714333.png"/><br/> ISO-8859-1:
UnicodeEncodeError: ‘gbk’ codec can’t encode character ‘\x87’ in position 11: illegal multibyte sequence

都没有效果<br/> 解决方法二：<br/> 可能是不认识的编码。于是按照《使用chardet判断编码方式》使用chardet进行编码自动判断并调用

```
import chardet

def chardets():
	path = 'C:\\Users\\Administrator\\Desktop\\案例二.docx'
	with open(path, 'rb') as f:
    	#print(chardet.detect(f.read())['encoding'])
    	return chardet.detect(f.read())['encoding']
#chardets()
with open('C:\\Users\\Administrator\\Desktop\\案例二.docx','r', 	encoding=chardets())as f:
	contents = f.read()
	print(contents)

```

然而依然保错：UnicodeDecodeError: ‘gbk’ codec can’t decode byte 0xe3 in position 55: illegal multibyte
sequence<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503144409480.png"/><br/> 看看是什么样的编码这样难以解决

```
print(chardet.detect(f.read())['encoding'])

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503144523767.png"/><br/> 怎么是None呢？

```
def chardets():
path = 'C:\\Users\\Administrator\\Desktop\\案例二.docx'
with open(path, 'rb') as f:
    print(chardet.detect(f.read()))#chardet.detect()返回的是一个字典，所以之前需要[‘encoding’]获取编码方式
    #return chardet.detect(f.read())['encoding']
chardets()

```

结果一样是None<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503144836703.png"/><br/>
于是我再次尝试了txt文件的读取，结果正常读取

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503145015565.png"/><br/> 但是有意思的是，其编码竟然是

```
{'encoding': 'TIS-620', 'confidence': 0.3598212120361634, 'language': 'Thai'}

```

这个编码从未见过，于是我想可能是文件中存在异常的编码（之前写入的不是“你好”这两个字符，而是一篇文章）<br/> 解决方法三：<br/> 编码解决不了，那就解决出现问题的编码，对之进行跳过。<br/> 增加errors=‘ignore’

```
import chardet

def chardets():
path = 'C:\\Users\\Administrator\\Desktop\\案例二.docx'
with open(path, 'rb') as f:
    print(chardet.detect(f.read()))
    return chardet.detect(f.read())['encoding']
#chardets()
with open('C:\\Users\\Administrator\\Desktop\\案例二.docx','r', encoding=chardets(), errors='ignore')as f:
contents = f.read()
print(contents)

```

结果乱码

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503145644817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
之后尝试过对文档内容进行删除，查找是否存在异常的内容。<br/> 结果删成了上面的“你好”两个字符还是报错或者乱码。

尝试二进制byte写入后再gbk、utf-8读取，结果全是二进制内容<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503145953742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

解决方法四（最终解决方法）：<br/> 既然一致出现解码错误，而在读取txt时发现其编码为TIS-620，我想是不是文件格式导致的问题，于是查了一下读取docx的模块，结果出现了docx读取的模块，看来就是文档格式导致的问题了。<br/>
于是按照《Python学习笔记(28)
-Python读取word文本》下载了python-docx<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200503150359383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
import docx
file=docx.Document("C:\\Users\\Administrator\\Desktop\\案例二.docx")
for para in file.paragraphs:
	print(para.text)

```

总结：有时错误是由于其上层错误导致的，而不是自己的问题，在找不到错误的情况下需要找找其上层依赖的问题是否存在。<br/> [1]https://blog.csdn.net/Katrina_ALi/article/details/80638972?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158848764019725256734556%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.57662%2522%257D&amp;request_id=158848764019725256734556&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2<sub>all</sub>first_rank_v2~rank_v25-6

【2】https://blog.csdn.net/woshisangsang/article/details/75221723?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_medium=distribute.pc_search_result.none-task-blog-2<sub>blog</sub>sobaiduweb~default-0
