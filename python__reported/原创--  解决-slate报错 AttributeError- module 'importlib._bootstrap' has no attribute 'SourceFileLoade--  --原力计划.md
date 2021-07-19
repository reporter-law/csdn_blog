# 原创

： 解决：slate报错 AttributeError: module 'importlib._bootstrap' has no attribute 'SourceFileLoade ：

原力计划

# 解决：slate报错 AttributeError: module 'importlib._bootstrap' has no attribute 'SourceFileLoade

在学习《python数据处理》时遇到了安装slate出错，这个问题不仅在slate、在之前按照pycurl时也出现，一直没有解决，原因差不多，都是这个报错，涉及python setup.py egg_info Check the logs
for full command output.<br/> 报错内容：

```
ERROR: Command errored out with exit status 1:
 command: 'C:\Users\Administrator\AppData\Local\Programs\Python\Python37\python.exe' -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'C:\\Users\\Administrator\\AppData\\Local\\Temp\\pycharm-packaging\\distribute\\setup.py'"'"'; __file__='"'"'C:\\Users\\Administrator\\AppData\\Local\\Temp\\pycharm-packaging\\distribute\\setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base 'C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\pip-egg-info'
     cwd: C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\
Complete output (15 lines):
Traceback (most recent call last):
  File "&lt;string&gt;", line 1, in &lt;module&gt;
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\setuptools\__init__.py", line 2, in &lt;module&gt;
    from setuptools.extension import Extension, Library
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\setuptools\extension.py", line 5, in &lt;module&gt;
    from setuptools.dist import _get_unpatched
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\setuptools\dist.py", line 7, in &lt;module&gt;
    from setuptools.command.install import install
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\setuptools\command\__init__.py", line 8, in &lt;module&gt;
    from setuptools.command import install_scripts
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\setuptools\command\install_scripts.py", line 3, in &lt;module&gt;
    from pkg_resources import Distribution, PathMetadata, ensure_directory
  File "C:\Users\Administrator\AppData\Local\Temp\pycharm-packaging\distribute\pkg_resources.py", line 1518, in &lt;module&gt;
    register_loader_type(importlib_bootstrap.SourceFileLoader, DefaultProvider)
AttributeError: module 'importlib._bootstrap' has no attribute 'SourceFileLoader'
----------------------------------------
ERROR: Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501201517711.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
原本试图通过查看报错信息来解决，不仅无法在pycharm中直接找到，而且这个是临时文件，去文件夹中也根本找不到。

网上的解决方法：《._bootstrap’ has no attribute ‘SourceFileLoader’ 和 ‘socketio’ has no attribute ‘Server’ 分析解决》、《python3出现module
“importlib._bootstrap” has no attribute “SourceFileLoader”》的解决方法基本都是“python -m ensurepip
--upgrade”，更新pip,setuotools,都没有效果。<br/>
还会遇上新的报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501201836991.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
即使我将mitmproxy卸载了，重新进行更新，也是一样<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501201940796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501201949806.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

参照《ubuntu18.0+python3.6+安装distribute模块出错（可能已解决）》，突然发现是不是我的python3.7不支持这个模块，也就是说这个模块比较老了，这个书《python数据处理》也是2017年，会不会遇到《python编程：从入门到实践》一样由于库的不更新导致不合时宜了。<br/>
于是，在pypi上寻找slate，果然发现slate仅更新到2016年。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501202311345.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

在github上找到作者，发现已经三年没有更新了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501203029125.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

在issue处发现。许多人都遇到这个问题，似乎都是与python3.4、3.5版本不兼容<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501203422762.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
最后也在问题的解答中找到了“pip install https://github.com/timClicks/slate/archive/master.zip
”从github上下载<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501203402215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

现在成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501203549682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

解决方法：找找github上的解答，又是应当是pip不支持，此时直接在github上下载即可

后续：虽然安装成功，但是由于没有更新，而其支持的pdfminer更新导致用起来很多问题

```
from .psparser import PSStackParser, PSSyntaxError, PSEOF, literal_name, LIT, KWD, handle_error
from .pdftypes import (PDFException, PDFTypeError, PDFNotImplementedError, PDFStream, PDFObjRef,
resolve1, decipher_all, int_value, str_value, list_value, dict_value, stream_value)
from .arcfour import Arcfour
from .utils import choplist, nunpack, decode_text, ObjIdRange

```

handle_error、str_value、
ObjIdRange都有问题，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501204953353.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501204957917.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501205453793.jpg"/>

需要修改的太多了，最后放弃了，不过或许可以下载之前的pdfminer来解决

最近更新为2019年。之前更新为2014年，下载2014年的，都下载失败了，下载20191010版本的成功了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501205632908.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501205701364.png"/><br/>
但是遇到报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501205719819.png"/>

```
        if PYTHON_3:
        self.doc = PDFDocument(self.parser)
        self.parser.set_document(self.doc)
        self.doc.set_parser(self.parser)
        self.doc.initialize(password)

```

加了一个self.parse进去<br/>
报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501210318278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
还是一样，需要修改的太多，最后放弃
