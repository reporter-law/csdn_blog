# 原创

： 从文本进度条开始：谈谈自己缺失的Python基础知识 ：

原力计划

# 从文本进度条开始：谈谈自己缺失的Python基础知识

### 从文本进度条开始：谈谈自己缺失的Python基础知识

# 一、文本进度条

在对π进行求值时看到了文本进度条，之前一直用的是tqdm模块。

来源：步平凡：《使用 PYTHON 实现Π的计算》，链接: [https://www.cnblogs.com/bpf-1024/p/10549896.html](https://www.csdn.net/).

源码：

```
from math import fabs           #导入数学模块
from time import perf_counter   #导入时间模块

def Bar(i):         #动态文本条
	N = pow(10,level)
	a = int((i/N)*50)
	b = 50 - a
	Y , N = '*' * a , '.' * b
	print("\r计算中：{:3.0f}% [{}-&gt;{}] {:.2f}s".format(2 * a,Y,N,perf_counter()),end='')



level = eval(input('计算Pi精确到小数点后几位数：'))
print('\n{:=^70}'.format('计算开始'))
a,b,pi,tmp = 1,1,0,1
i = 0
'''
	a 分子  |  b 分母  |  pi 圆周率
	tmp 存储a/b的值    |  i  执行进度
'''
perf_counter()      #开始计时
while (fabs(tmp) &gt;= pow(10,-level)): #计算Pi
	pi += tmp
	b += 2
	a = -a
 	tmp = a/b
 	i += 2
	Bar(i)        #调用函数，实时显示计算进度
print('\n{:=^70}'.format('计算完成'))
print('\nPi的计算值为：{}'.format(round(pi*4,level))) #输出计算结果

```

对于Bar(i)
表示看不懂，就又去找了一个glitterye：《用python实现单行动态刷新文本进度条》，链接: [link](https://blog.csdn.net/JessiFan/article/details/82316256?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
.

# 二、基础知识

## （一）Python center()方法

菜鸟教程：链接: [link](https://www.runoob.com/python/att-string-center.html).

```
str = '2020'
print(str.center(20))#20为宽度
print(str.center(20,'-'))#'-'为填充内容

```

通过尝试明白了，center()方法是居中输出<br/> str.center(width[, fillchar])<br/> width – 字符串的总宽度。<br/> fillchar – 填充字符。

## （二）time.perf_counter()

```
经过尝试发现这是一个计时器，但是初始的print(time.perf_counter())并不为0
import time
print(time.perf_counter())
time.sleep(5)
print(time.perf_counter())

```

## （三）print()

菜鸟教程：链接: [link](https://www.runoob.com/python3/python-func-print.html).

```
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
objects -- 复数，表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
sep -- 用来间隔多个对象，默认值是一个空格。
end -- 用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。
file -- 要写入的文件对象。
flush -- 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流	会被强制刷新。

```

尝试：

```
for i in range(10):
print('\r',i,end='')
#因为默认的结尾为'\n’，所以改变导致更新

```

虽然之前见过end=’’,但是一直不明其里，只是知道可以不换行，而对于\r见过但是没有用过，之前一直按照《Python编程：从入门到实践》用过\t \n,到此处才明白，\r相当于回车。

但是对于flush不怎么理解，True或者False效果一样

```
print(".",end = '',flush=True)

```

```
print(".",end = '',flush=False)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200513165449295.png"/><br/> 一样是一个一个点刷新

并不像energy_百分百：《#深入理解# python 的 print() 函数 在当前行打印 不换行》说的一次性刷新六个点（ps:
难道我的理解有误），链接: [link](https://blog.csdn.net/lch551218/article/details/105446636?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=flush%20--%20%E8%BE%93%E5%87%BA%E6%98%AF%E5%90%A6%E8%A2%AB%E7%BC%93%E5%AD%98%E9%80%9A%E5%B8%B8%E5%86%B3%E5%AE%9A%E4%BA%8E%20file%EF%BC%8C%E4%BD%86%E5%A6%82%E6%9E%9C&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-4-105446636)
.

# 三、练习的代码

```
import time
scale = 50
print("执行开始".center(scale // 2,"-"))#中心显示
start = time.perf_counter()#计时器
for i in range(scale + 1):
a = "*" * i
#*随着循环递增
b = "." * (scale - i)
#随着循环递减
c = (i / scale) * 100
# c为前面的百分比
dur = time.perf_counter() - start
print("\r{:^3.0f}%[{}-&gt;{}]{:.2f}s".format(c,a,b,dur),end = "")

time.sleep(0.1)
print("\n"+"执行结束".center(scale // 2,"-"))
for i in range(10):
	print('a \r a',i,end='')
#因为默认的结尾为'\n’，所以改变导致更新

```
