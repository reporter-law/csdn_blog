# 原创

： 列表数据清洗遇到问题的记录——set用法和remove方法的缺陷

# 列表数据清洗遇到问题的记录——set用法和remove方法的缺陷

爬虫过程中会由于各种原因导致数据重复以及确实，如网络中断，网络质量差，ip限制等等，因而进行数据清洗十分必要。<br/> 在这个爬虫中，由于ip限制，为了尽量保证数据的完整性，尽量收集最多的数据，因而具有明显的重复率。<br/>
重复率清洗的思路：<br/> 1、初始的思路是按照选择排序法进行删重（刚刚学了选择排序法想用一下且没有想起set）<br/>
对选择排序法进行改造<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200413215039932.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
初始的想法就是将 if data[i] &gt; data[j]:这个if语句改为if data[i] == data[j]：，以实现重复内容的删除。<br/> 问题：<br/>
这里遇到的问题就是没有正确理解选择排序法的含义，将i的取值等于整个数据列表的长度而不是该长度-1
，因为i代表前一个元素，因而其不能遍历到最后一个元素，因而对i的赋值需要比元素的个数少一个；而与之相反，j的取值则需要减少第一个元素而保留最后一个元素，因而为for j in (i+1,len(url)):

这个问题的失误导致报错：IndexError: list index out of range<br/>
示例：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200413215703249.png"/><br/> IndexError: list index out
of range的解决：<br/>
许多博文都提到，这个报错是由于越界或者空值，即列表索引超出列表元素个数的数组越界和该索引的元素为空值，而在这个爬虫中明显不可能是空值，因而只可能是数组越界，也是由此才重新去细看了选择排序法并理解了它。<br/>
其次，为remove语句存在的问题，<br/> 报错：ValueError: list.remove(x): x not in list<br/> 找了许多文章，很多都没有用，比如<br/>
《pycharm的python文件报“ValueError: list.remove(x): x not in list”错误》的方法其实就是一个掩耳盗铃的方法，一般使用了grep
console的报错会有颜色，这篇文章的解决方法就是要颜色不要显示！！！

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200412194534846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
以下这篇为有用的博文：<br/> 《python:在for遍历list时使用remove出现的问题以及解析》<br/>
我的理解为：列表元素删除后产生一个新列表，就是原列表的删除元素后组成的列表，每次删除都会形成这样一个新列表；但是索引仍为原列表索引就是遗漏。

虽然找到了remove的局限性，并参照另一篇《Python列表的remove方法的注意事项》进行尝试解决，但是我没有用其中的方法，而是尝试对原列表进行了复制<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200413221004633.png"/><br/>
然后依据原列表的重复元素在副本列表中进行删除<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041322112168.png"/><br/>
但是这个报错还是出现了，大致在第13个重复元素中，照理说并应该存在问题——希望大神能够指出！！！！！！！！！！！！！！！！！！！！！！！！

于是我用try: except：进行异常的跳过，跳过后重复元素确实删除了，但是不知道为什么多删了一个不重复的元素。

在这条路走不通后，突然想起了set函数，现在终于解决了！！！！<br/> 但是对于第二个报错始终不理解，留待后续。。。。。。。。。

[1]https://blog.csdn.net/circle2015/article/details/64444300?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158678637719724845025972%2522%252C%2522scm%2522%253A%252220140713.130102334…%2522%257D&amp;request_id=158678637719724845025972&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task-blog-soetl_SOETLBAIDU-3

[2]http://blog.sina.com.cn/s/blog_678b56660102w6tp.html

[3]https://blog.csdn.net/qq_41612692/article/details/88833386?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158678637719724845025972%2522%252C%2522scm%2522%253A%252220140713.130102334…%2522%257D&amp;request_id=158678637719724845025972&amp;biz_id=0&amp;utm_source=distribute.pc_search_result.none-task-blog-soetl_SOETLBAIDU-2
