# 原创

： python运行加速的几种方式

# python运行加速的几种方式

### python运行加速的几种方式

# 一、总结

1、使用pypy<br/> 2、减少函数化调用<br/> 3、减少文件的打开即with的调用，将这一调用放在for循环前面，然后传递至后面需要用到的地方<br/> 4、if函数判断条件多的尽量在前面<br/> 全面加速（pypy)

# 二、全面加速（pypy)

将python换为pypy,在纯python代码下，pypy的兼容性就不影响使用了，因为一些纯python的代码常常会用pypy进行一下加速

测试代码，for循环10000000次

```
start = time.time()
for i in range(10000000):
    print(i,end="\r")
end = time.time()
print(f"耗费时间{end-start}秒&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;")

```

pypy的耗时为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711215317702.png"/><br/>
而python耗时为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711220249277.png"/><br/>
大致三倍，但是循环越多估计越快，据说有6倍左右

# 二、减少文件的打开即with的调用

原代码的with在调用函数内，即每次调用函数都要打开并关闭文件，造成大量耗时

```

def BMES(word,tag):
    with open(r"J:\PyCharm项目\学习进行中\NLP教程\NLP教程\数据集\词性标注\nature2ner.txt","a+",encoding="utf-8")as f_:
        if len(word) == 1:
            """单字"""
            f_.write(word + " " + f"S-{tag.upper()}" + "\n")
        else:
            """多字"""
            for index, word_ in enumerate(word):
                if index == 0:
                    f_.write(word_ + " " + f"B-{tag.upper()}" + "\n")
                elif 0 &lt; index &lt; len(word) - 1:
                    f_.write(word_ + " " + f"M-{tag.upper()}" + "\n")
                else:
                    f_.write(word_ + " " + f"E-{tag.upper()}" + "\n")

#后续在多个if-elif-else中调用

```

耗时为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711220748923.png"/><br/> tqdm预估时间在15~25个小时左右跳动

将with放在循环前面<br/> 如<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711225331552.png"/><br/> 将with的内容作为f_
传递进来

后的耗时为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711225307780.png"/>

测试如下：

```
import os, warnings,time,tqdm
def txt(word):
    with open("ceshi.txt","a+",encoding="utf-8")as f:
        if len(str(word))&lt;=2:
            word+=100
            f.write(str(word)+"\n")
        elif 2&lt;len(str(word))&lt;=4:
            word+=200
            f.write(str(word)+"\n")
        else:
            f.write(str(word) + "\n")
if __name__=="__main__":
    start = time.time()
    for i in tqdm.tqdm(range(100000)):
        txt(i)
    end = time.time()
    print(f"耗费时间{end-start}秒&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;")

```

耗时结果为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711222347872.png"/><br/> 将文件的打开即with的调用放在外面

```
import os, warnings,time,tqdm
def txt(f,word):

        if len(str(word))&lt;=2:
            word+=100
            f.write(str(word)+"\n")
        elif 2&lt;len(str(word))&lt;=4:
            word+=200
            f.write(str(word)+"\n")
        else:
            f.write(str(word) + "\n")
if __name__=="__main__":
    start = time.time()
    with open("ceshi.txt", "a+", encoding="utf-8")as f:
        for i in tqdm.tqdm(range(100000)):

            txt(f,i)
    end = time.time()
    print(f"耗费时间{end-start}秒&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;")

```

耗时为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210711222858785.png"/><br/> 结论：快了119倍，而实际加速远远大于这个倍数

# 三、if判断靠前

如：

```
 if tag in ["nts", "nto", "ntc", "ntcb", "ntcf", "ntch", "nth", "ntu", "nt"]:
                                BMES(f_,i2, tag="ORG")
                            elif tag in ["nb", "nba", "nbc", "nbp", "nf", "nm", "nmc", "nhm", "nh"]:
                                BMES(f_,i2, tag="OBJ")
                            elif tag in ["nnd", "nnt", "nn"]:
                                BMES(f_,i2, tag="JOB")
                            elif tag in ["nr", "nrf"]:
                                BMES(f_,i2, tag="PER")
                            elif tag in ["t"]:
                                BMES(f_,i2, tag="TIME")
                            elif tag in ["ns", "nsf"]:
                                BMES(f_,i2, tag="LOC")
                            else:
                                for i3 in list(i2):
                                    f_.write(i3 + " " + f"O" + "\n")

```

满足条件的可以先跳出判断
