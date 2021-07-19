# 原创

： 重装系统后python环境问题后续——scrapy生成spider报错：Fatal error in launcher: Unable to create process using

# 重装系统后python环境问题后续——scrapy生成spider报错：Fatal error in launcher: Unable to create process using

### 重装系统后python环境问题后续：scrapy

# 报错：Fatal error in launcher: Unable to create process using’“c:\users\administrator\appdata\local\programs\python\python37\python.exe” “D:\Users\Administrator\AppData\Local\Programs\Python\Python37\Scripts\scrapy.exe” startproject spider’: ???

<img alt="你好！ 这是你第一次使用 **Markdown编辑器** 所展示的欢迎页。如果你想学习如何使用Markdown编辑器, 可以仔细阅读这篇文章，了解一下Markdown的基本语法知识。" src="https://img-blog.csdnimg.cn/20200510085341161.png"/><br/>
原因似乎是找不到python解释器的路径

# 解决路径

首先，需要确定python的环境变量已经添加<br/>
如：输入python,进入python编辑器<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510085800454.png"/><br/>
如果没有就将之加入环境变量中，达到如上效果

其次，在scrapy前增加python -m

```
python -m startproject spider(ps:换成自己的spider的名字）

```

最后，成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200510090007685.png"/><br/> 每次加上python -m
也挺麻烦，不知道大家有没有直接解决的办法！！！！！！！！！！！！！！！！！

参见《Scrapy Fatal error in launcher: Unable to create process
using》<br/> [1]:https://blog.csdn.net/qq_41988893/article/details/103118573?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158907116919724811853738%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&amp;request_id=158907116919724811853738&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2<sub>all</sub>first_rank_v2~rank_v25-1-103118573.nonecase&amp;utm_term=scrapy+%E9%81%87%E5%88%B0+Fatal+error+in+launc
