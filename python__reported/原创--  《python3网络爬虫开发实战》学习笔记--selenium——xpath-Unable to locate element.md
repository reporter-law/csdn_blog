# 原创

： 《python3网络爬虫开发实战》学习笔记：：selenium——xpath：Unable to locate element

# 《python3网络爬虫开发实战》学习笔记：：selenium——xpath：Unable to locate element

selenium+firefox在定位时遇到selenium.common.exceptions.NoSuchElementException: Message: Unable to locate element:

由于是js加载页面，想确认是否是js的原因，随后进行多次调试时发现“//div”竟然也出现了selenium.common.exceptions.NoSuchElementException: Message: Unable to
locate element:
//div或者是【】：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200403151922607.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200403152206948.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200403152334213.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200403152353509.png"/><br/>
这种定位错误一般很少出现，因为其中的xpath路径一般是通过copy xpath而不是自己写的。<br/> 就现在而言，这种copy 过来的xpath定位不了主要有以下几个原因：<br/>
1、该网页的标签存在拼写错误时会定位不到，在某个网页的标签为abady是遇到过定位不了<br/> 解决方法：去除该拼写错误的标签，然后进行一定的xpath路径调整

还有一个暂时没有想到…等想到了在补充进来！
