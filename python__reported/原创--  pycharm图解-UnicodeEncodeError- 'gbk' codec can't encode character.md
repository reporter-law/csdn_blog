# 原创

： pycharm图解：UnicodeEncodeError: 'gbk' codec can't encode character

# pycharm图解：UnicodeEncodeError: 'gbk' codec can't encode character

python运行报错<br/> UnicodeEncodeError: ‘gbk’ codec can’t encode character ‘\xa0’ in position 111523: illegal multibyte
sequence

指定encoding=utf-8或者gbk,乃至网页编码<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330172921362.png"/><br/>
以及将r.encoding = r.apparent_encoding,都没有效果，只有将内容写入txt文本时才没有报错。但是在需要在控制台查阅时就会非常不方便。<br/> 于是学习了一下编码知识。<br/>
参考以下三篇文章后找到了解决方法：<br/>
博主爱撒谎的男孩的《python中decode和encode的区别》“字符串在Python内部的表示是unicode编码，因此，在做编码转换时，通常需要以unicode作为中间编码，即先将其他编码的字符串解码（decode）成unicode，再从unicode编码（encode）成另一种编码。”

博主极客之道《UnicodeEncodeError: ‘gbk’ codec can’t encode character ‘\xa0’ in position …
问题解决办法之一》网络数据流写入文件时的三个编码，python文件的编码、网页编码、写入文件编码

博主CN-LILU《‘gbk’ codec can’t encode character ‘\xa0’ in position 12248: illegal multibyte sequence》print()
函数自身有限制，不能完全打印所有的unicode字符

首先检测是否print()函数限制问题，不过基本不可能。print(‘results’ == ‘\u0061’)的验证结果为false。<br/> 其次，网页写入的编码方式也是正确的，因为print(r.encoding)
的编码为utf-8.<br/>
最后，受到前两个博主的文章启发想到是否是console呈现的编码不正确，即console的编码为gbk，gbk无法解码\xa0。因为在python中需要Unicode的中转，网页数据流写入python需要decode，python写入其他文件需要encode,因而console呈现的可能也是需要python进行encode的内容，这里的问题就在于console的encode出现问题。在pycharm中发现确实如此，因为之前为了在ternimal中呈现中文而不是乱码,所以将命令行的编码均设置为gbk。现在gbk无法将position
111523的’\xa0’ 呈现，需要将gbk换成utf-8.这个设置在pycharm的设置中，设置的编辑器的文本编码中。

具体解决方法如下图<br/> 第一步：点击文件打开编辑器<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330180737289.png"/>

第二步：打开编辑器的文本编码进行修改<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330180842402.png"/><br/> 第三步：将Global
Encoding改回utf-8(
需要ternimal不乱码需要改回）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330181005843.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330181025632.png"/>

改变了编码方式后没有了报错：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200330181117114.png"/>
