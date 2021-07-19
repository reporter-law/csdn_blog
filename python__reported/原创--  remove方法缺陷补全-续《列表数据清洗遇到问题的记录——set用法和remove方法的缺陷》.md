# 原创

： remove方法缺陷补全：续《列表数据清洗遇到问题的记录——set用法和remove方法的缺陷》

# remove方法缺陷补全：续《列表数据清洗遇到问题的记录——set用法和remove方法的缺陷》

### remove方法缺陷补全：续《列表数据清洗遇到问题的记录——set用法和remove方法的缺陷》

# 一、问题

remove方法缺陷：需要删除的内容没有办法完全删除<br/>
现象：见上一篇文章《列表数据清洗遇到问题的记录——set用法和remove方法的缺陷》，链接: [link](https://blog.csdn.net/python__reported/article/details/105474708)
.

上一次的可以通过set进行重复值剔除，但是此次不是重复值剔除，不能运用set方法，出现了剔除不干净

这次是我在进行jieba分词的停用词处理时遇到的问题，不能用set方法的重复值剔除。<br/> 如下，停用词中加入了“本院”，

希望进行该词的剔除，<br/> 原始代码（部分）：

```
        for value in lst_words:
        #print(lst_words)
        if value in stop_word:
            lst_words.remove(value)

```

下图为没有进行删除前的“本院”的数量，大致12个<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200526155504808.png"/><br/>
下图为进行删除的“本院”的剩余数量为3个

“本院”数量由12个变成了3个，可见remove方法进行了该词的清除，但是没有清除干净。<br/>
一开始没有发现是remove方法的问题，认为可能是某些“本院”这个词语的格式有些不对，比如多了空格之类的，找了半天，发现没有问题，这是才想到了可能是remove的问题

# 二、解决方法

解决方法非常简单，但是在上一篇用时没有想到。既然一次清不干净就多清几次，使用for循环

```
        for i in range(3):
        for value in lst_words:
        #print(lst_words)
            if value in stop_word:
                lst_words.remove(value)
            #本院没有完全去掉，是否是remove导致的
                index += 1
            else:
                pass	

```

尝试完全清楚大约要三次，for循环就来了四次，怕其他数据清洗时存在问题

之后就清理干净了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200526160354713.png"/>
