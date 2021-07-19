# 原创

： python机器学习基础教程第七章Traceback (most recent call last):OSError: [E050] Can‘t find model ‘en‘.

# python机器学习基础教程第七章Traceback (most recent call last):OSError: [E050] Can‘t find model ‘en‘.

### OSError: [E050] Can't find model 'en'.

# 一、问题

初次导入spacy的英语模型时报错：

```
Traceback (most recent call last):
File "... ...", line 12, in &lt;module&gt;
en_nlp = spacy.load('en')
 File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\spacy\__init__.py", line 30, in load
return util.load_model(name, **overrides)
 File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\spacy\util.py", line 175, in load_model
raise IOError(Errors.E050.format(name=name))
OSError: [E050] Can't find model 'en'. It doesn't seem to be a shortcut link, a Python package or a valid path to a data directory.

```

这个模型没有随着spacy下载而下载，因而需要单独下载<br/> 书中建议：

```
python3 -m spacy download en

```

但是遇到这个错误：

```
Traceback (most recent call last):
 File "C:\Users\lenovo\AppData\Roaming\Python\Python37\site-packages\urllib3\contrib\pyopenssl.py", line 456, in wrap_socket
cnx.do_handshake()
 File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\OpenSSL\SSL.py", line 1934, in do_handshake
self._raise_ssl_error(self._ssl, result)
File "D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\OpenSSL\SSL.py", line 1663, in _raise_ssl_error
raise SysCallError(errno, errorcode.get(errno))
OpenSSL.SSL.SysCallError: (10054, 'WSAECONNRESET')

```

SSL验证失败

# 二、方法

找到spacy中的download.py这个文件<br/>
第一步：找到spacy这个包<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210103155806230.png"/><br/>
第二步找到cli这个模块<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210103155914538.png"/><br/>
第三步：在cli模块中找到download.py这个文件<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210103160001817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第四步：修改download.py中第95行的源码，增加verify=False，跳过验证<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210103160110757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、下载成功

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2021010316024163.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
导入不报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210103160315114.png"/>
