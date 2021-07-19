# 原创

： python3网络爬虫开发实战

# python3网络爬虫开发实战

适用命令行pip install tesserocr 安装tesserocr时出现报错Microsoft Windows [版本 6.1.7601]<br/> 版权所有 © 2009 Microsoft
Corporation。保留所有权利。

C:\Users\Administrator&gt;pip install tesserocr<br/> Collecting tesserocr<br/> Using cached tesserocr-2.5.0.tar.gz (54
kB)<br/> Building wheels for collected packages: tesserocr<br/> Building wheel for tesserocr (setup.py) … error<br/>
ERROR: Command errored out with exit status 1:<br/> command: ‘c:
\users\administrator\appdata\local\programs\python\python38-32\py<br/> thon.exe’ -u -c ‘import sys, setuptools,
tokenize; sys.argv[0] = ‘"’"‘C:\Users<br/>
\Administrator\AppData\Local\Temp\pip-install-kv0214pl\tesserocr\setup.py’<br/> "’"’; **file**=’"’"‘C:
\Users\Administrator\AppData\Local\Temp\pip-install-<br/> kv0214pl\tesserocr\setup.py’"’"’;f=getattr(tokenize, ‘"’"
‘open’"’"’, open)(**f<br/> ile**);code=f.read().replace(’"’"’\r\n’"’"’, ‘"’"’\n’"’"’);f.close();exec(compil<br/> e(
code, **file**, ‘"’"‘exec’"’"’))’ bdist_wheel -d ‘C:\Users\Administrator\AppDa<br/>
ta\Local\Temp\pip-wheel-ky53j_jh’<br/> cwd: C:\Users\Administrator\AppData\Local\Temp\pip-install-kv0214pl\tesse<br/>
rocr<br/> Complete output (12 lines):<br/> C:
\Users\Administrator\AppData\Local\Temp\pip-install-kv0214pl\tesserocr\setup<br/> .py:72: SyntaxWarning: “is not” with a
literal. Did you mean “!=”?<br/> if subversion is not None and subversion is not “”:<br/> C:
\Users\Administrator\AppData\Local\Temp\pip-install-kv0214pl\tesserocr\setup<br/> .py:134: DeprecationWarning: The
‘warn’ method is deprecated, use ‘warning’ inst<br/> ead<br/> _LOGGER.warn(‘Failed to extract tesseract version from
executable: {}’.forma<br/> t(e))<br/> Failed to extract tesseract version from executable: [WinError 2] 系统找不到指<br/>
定的文件。<br/> Supporting tesseract v3.04.00<br/> Building with configs: {‘libraries’: [‘tesseract’, ‘lept’],
‘cython_compile_ti<br/> me_env’: {‘TESSERACT_VERSION’: 50593792}}<br/> running bdist_wheel<br/> running build<br/>
running build_ext<br/> building ‘tesserocr’ extension<br/> error: Microsoft Visual C++ 14.0 is required. Get it with "
Microsoft Visual C+

ERROR: Command errored out with exit status 1: ‘c:\users\administrator\appdata\l<br/>
ocal\programs\python\python38-32\python.exe’ -u -c ‘import sys, setuptools, toke<br/> nize; sys.argv[0] = ‘"’"‘C:
\Users\Administrator\AppData\Local\Temp\pip-ins<br/> tall-kv0214pl\tesserocr\setup.py’"’"’; **file**=’"’"‘C:
\Users\Administrator<br/> \AppData\Local\Temp\pip-install-kv0214pl\tesserocr\setup.py’"’"’;f=getattr(<br/> tokenize, ‘"
’"‘open’"’"’, open)(**file**);code=f.read().replace(’"’"’\r\n’"’"’,<br/> ‘"’"’\n’"’"’);f.close();exec(compile(code, **
file**, ‘"’"‘exec’"’"’))’ install -<br/> -record ‘C:
\Users\Administrator\AppData\Local\Temp\pip-record-8sn912s2\install-r<br/> ecord.txt’
--single-version-externally-managed --compile --install-headers ‘c:\u<br/>
sers\administrator\appdata\local\programs\python\python38-32\Include\tesserocr’<br/> Check the logs for full command
output.

然后找了一上午的解决方法，包括寻找版本是否正确、配置环境变量等等！。<br/>
当时在找版本配置时我就奇怪为什么所有说版本配置的都是python3.7及以下的，完全没有看见有3.8版本的。只是以为没有找到最新版本的下载地址而已，于是继续去找了tesserocr-2.5.0.tar（ps:
其实pip下载的也是这个版本，我下载的teseract是最新版的，不过下载旧版的估计也不行，因为我的python版本是3.8的）。下载下来的tesserocr-2.5.0.tar在命令行使用pip install
+（文件名拖拽过来的地址）还是不行，报错的内容是不适应这个平台。这时我才反应过来，tesserocr可能有问题，但是我并不知道它的新名字。<br/>
兜兜转转又是重新下载旧版的teseract和tesserocr，以及按照博主的文章配置环境变量等等，还是失败了。直到找到19年的关于配置teseract出现了pyteseract才知道原来的tesserocr换了一个名字。<br/>
之后的安装过程就和书上差不多，只是将tesserocr换成pyteseract，然后使用pip安装，只是需要修改一点点内容，可以参见https://blog.csdn.net/Dongzizhu/article/details/100805894?depth_1-utm_source=distribute.pc_relevant.none-task&amp;utm_source=distribute.pc_relevant.none-task。<br/>
还有就是image_to_text变成了image_to_string。其它的暂时没有发现问题。
