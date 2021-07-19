# 原创

： 解决方法集锦：requests.exceptions.ChunkedEncodingError

# 解决方法集锦：requests.exceptions.ChunkedEncodingError

运行程序报错；<br/> File “C:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\requests\models.py”,
line 754, in generate<br/> raise ChunkedEncodingError(e)<br/> requests.exceptions.ChunkedEncodingError: (“Connection
broken: ConnectionResetError(10054, ‘远程主机强迫关闭了一个现有的连接。’, None, 10054, None)”, ConnectionResetError(10054,
‘远程主机强迫关闭了一个现有的连接。’, None, 10054, None))

大概每隔15-30分钟就会出现一次<br/> 一般还会有requests.exceptions.ChunkedEncodingError: (‘Connection broken: IncompleteRead(1609 bytes
read)’, IncompleteRead(2753 bytes expect))

解释；似乎是连接中断，解码只解了一半的意思

许多方法都是<br/> CSDN博主「BelieverH」《requests.exceptions.ChunkedEncodingError: (‘Connection broken: IncompleteRead(0 bytes
read)’, IncompleteRead(0 bytes read))解决方法：<br/> 问题：爬虫requests请求时发生如下错误》<br/> 的这种方法：<br/> r = requests.post(url=read_url,
headers=headers, proxies=it, stream=True)<br/> 我使用过，这种方法对我的问题没有作用！！！！

因为这种似乎是针对0 bytes read,即一开始就读取失败的<br/> 但是我的不是。

第二种方法<br/> 增加版本声明，这是由于http1.0与1.1的不同<br/> 博主甜甜圈Sweety；《requests.exceptions.ChunkedEncodingError: (‘Connection broken:
IncompleteRead(0 bytes read)’, Incomp》提供的解决方法：<br/> 所以解决方案可以有很多：<br/> 1.修改python源码，把报错去掉（去掉后如果你的代码没有问题，就可以传输了）<br/>
2.使用http1.0来进行request<br/> 3.不用requests，用python curl等等。<br/> 4.也许更新python的requests库会有用。<br/> 5.加版本声明：

```
import httplib
httplib.HTTPConnection._http_vsn = 10
httplib.HTTPConnection._http_vsn_str = 'HTTP/1.0'

```

python3应当更改为：<br/> 博主Luopan13《Connection broken: IncompleteRead(1394 bytes read)’, IncompleteRead(1394 bytes read)》

```
import http.client
http.client.HTTPConnection._http_vsn = 10
http.client.HTTPConnection._http_vsn_str = 'HTTP/1.0'

```

尝试过无效

后来一直没有解决，只有深入models.py中去进行源码修改，修改思路：就是简单的函数回调

现在运行了3个多小时无事！！！！！！

【1】https://blog.csdn.net/u010351326/article/details/102704206?depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-5&amp;utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-5<br/>
【2】https://blog.csdn.net/qinglingls/article/details/96476151
