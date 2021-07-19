# 原创

： 词云（wordcloud）报错：ValueError: We need at least 1 word to plot a word cloud, got 0. ：

原力计划

# 词云（wordcloud）报错：ValueError: We need at least 1 word to plot a word cloud, got 0.

### 词云（wordcloud）报错：ValueError: We need at least 1 word to plot a word cloud, got 0.

# 一、现象

```
代码：
		
		import wordcloud
		sentence = 'I like you '
		wc = wordcloud.WordCloud()
		wc.generate(sentence)
		wc.to_file('test.png')

```

报错：

```
ValueError: We need at least 1 word to plot a word cloud, got 0.

```

但是换一下：

```
import wordcloud
		sentence = '尺寸超差错错错错错错错错错错错错错错错错错错 '
		wc = wordcloud.WordCloud(font_path='msyh.ttc')
		wc.generate(sentence)
		wc.to_file('test.png')

```

不报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200513083315923.png"/><br/> 生成图片：

# 二、尝试解决

## （一）尝试解决方法一

在github中找到了一个方法，方法是修改源码中的正则表达式<br/> 链接: [link](https://github.com/amueller/word_cloud/issues/495).

源码：

```
regexp = self.regexp if self.regexp is not None else r"\w[\w']+"

```

在 File “D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\wordcloud\wordcloud.py”,
（我的python在D盘，需要找到自己的site-packages\wordcloud\wordcloud.py的第573行，修改为\w+<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051308503336.png"/><br/>
即

```
regexp = self.regexp if self.regexp is not None else r"\w+"

```

但是这样还是没有解决问题，只读了一个单词

## （二）尝试解决方法二

既然可能是正则的问题，又重新查了一下

```
\w+:是指匹配一个以上的任意字母、数字及下划线

```

照理说这里有八个字母，应当匹配上，尝试去掉空格

```
import wordcloud
sentence = 'Ilikeyou '
wc = wordcloud.WordCloud()
wc.generate(sentence)
wc.to_file('test.png')

```

没有报错：

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200513090255904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
是空格的问题吗？加上下划线，看看怎么样

```
import wordcloud
sentence = 'Ilikeyou '
wc = wordcloud.WordCloud()
wc.generate(sentence)
wc.to_file('test.png')

```

也OK！！<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200513090530720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
要把空格加上只能将源码修改为

```
regexp = self.regexp if self.regexp is not None else r".+"

```

修改后没有报错，且存在空格<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051309081867.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

但是可能会影响到其他使用，因而最好还是不要更改。

# 三、最终结论

按照需求更改正则表达式<br/> 修改地址为：

```
"D:\Users\Administrator\AppData\Local\Programs\Python\Python37\lib\site-packages\wordcloud\wordcloud.py", （ps:我的python在D盘，需要找到自己的site-packages\wordcloud\wordcloud.py的第573行，修改这一行的正则表达式）

```
