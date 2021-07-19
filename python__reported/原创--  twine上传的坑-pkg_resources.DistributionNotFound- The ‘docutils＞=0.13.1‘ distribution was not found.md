# 原创

： twine上传的坑：pkg_resources.DistributionNotFound: The ‘docutils＞=0.13.1‘ distribution was not found

# twine上传的坑：pkg_resources.DistributionNotFound: The ‘docutils＞=0.13.1‘ distribution was not found

### twine上传的坑：pkg_resources.DistributionNotFound: The 'docutils&gt;=0.13.1' distribution was not found

# 一、制作pypi模块

## （一）注册pypi账号

## （二）设置setup.py

```
from setuptools import setup, find_packages

```

setup(<br/> # pip install nnn<br/> name=“crawler_tools”,#上传的包名<br/> version=“0.0.3”,#包的版本号<br/> #以下均为介绍<br/> keywords=(
“crawler”, “tools”, “proxy”,“cookies”,“user-agent”),<br/> description=“爬虫工具”,<br/>
long_description=“爬虫工具集合，其中代理用的是崔庆才的代理池和jhao的代理池，而cookies和user-agent是自己的创作，总体上是在综合”,<br/> # 协议<br/> license=“GPL
Licence”,

```
url="",
author="cw",
author_email=""#作者联系邮箱,

# 自动查询所有"__init__.py"
python_requires = '&gt;=3.5.*',#pythonb版本
packages=find_packages(),
include_package_data=True,
platforms="any",
# 提示前置包
install_requires=['selenium',
                  'requests',
                  'APScheduler',
                  'werkzeug==0.15.3',
                  'Flask',
                  'lxml',
                  'PyExecJS',
                  'click',
                  'gunicorn==19.9.0',
                  'redis',
                  'environs==7.2.0',
                  'attrs',
                  'retrying',
                  'aiohttp==3.6.2',
                  'loguru==0.3.2',
                  'pyquery',
                  'supervisor',
                  ]

```

)

## （三）打包命令

```
python setup.py sdist

```

这个要在setup.py的路径下，比如我要打包的是crawler_tools这个包，同级目录中建立如上所述的setup.py文件<br/>
在这里插入图片描述<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200823155529758.png#pic_center"/>

打包后形成<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020082315532224.png#pic_center"/>

# 二、上传

```
twine upload 自己的包名如：C：/crawler_tools-0.0.3.tar.gz

```

这里遇到一个比较奇葩的问题<br/> 报错如下：

```
pkg_resources.DistributionNotFound: The 'docutils&gt;=0.13.1' distribution was not found and is required by readme-renderer

```

这是在python3.8中的报错<br/> 但是我虽然装了两个python，但是python3.8不在我的环境变量中<br/>
在这里插入图片描述<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020082315580612.png#pic_center"/><br/>
我的twine也在装在python3.7的目录中

但是出现如上报错就感觉十分奇葩<br/> 最后去python3.8中下载了这个包才好
