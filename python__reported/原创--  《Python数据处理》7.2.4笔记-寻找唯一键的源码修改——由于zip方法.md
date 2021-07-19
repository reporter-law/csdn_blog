# 原创

： 《Python数据处理》7.2.4笔记：寻找唯一键的源码修改——由于zip方法

# 《Python数据处理》7.2.4笔记：寻找唯一键的源码修改——由于zip方法

### 《Python数据处理》7.2.4笔记：寻找唯一键的源码修改——由于zip方法

# 一、原因：zip方法

参考《python中使用zip函数出现》,原因是为了节约内存，python3基于此对此进行了优化，输出只输出对象的内存位置而不打印出来。而在python2中可以直接输出到屏幕，<br/> 解决方法：需要增加list

源码：

```
set_keys = set(
        ['%s-%s-%s' % (x_[0][1], x_[1][1], x_[2][1]) for x_ in zipped_data]
    )#原为x,c此处改为x_
unique = [x_ for x_ in  zipped_data
              if not set_keys.remove('%s-%s-%s' % (x_[0][1], x_[1][1], x_[2][1]))
              ]

```

z直接运行报错：TypeError: ‘zip’ object is not
subscriptable<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200514202750117.png"/>

# 二、修改后

```
注：将之前的zipped_data变成了调用的函数，change_title()即为zipped_data
def unique_value():
'''确定唯一值'''
try:
    x_list = []
    for x in change_title():
        x_list.append(list(x))
        # print(x_)
        '''由于zip()的输出需要list（）化'''
    set_keys = set(
        ['%s-%s-%s' % (x_[0][1], x_[1][1], x_[2][1]) for x_ in x_list]
    )
    print(len(set_keys))

    unique = [x_ for x_ in x_list
              if not set_keys.remove('%s-%s-%s' % (x_[0][1], x_[1][1], x_[2][1]))
              ]
    '''此处not的含义在于保障移除，且unique为唯一值的变量，如果少了not就会变成空集，因为均被移除'''
    pprint.pprint(unique)
    print('存在唯一值-----------------------------------------------------------------------')
except:
    print('不存在唯一值------------------------------------------------')

```

在这个列表推导式中：

```
unique = [x_ for x_ in x_list
              if not set_keys.remove('%s-%s-%s' % (x_[0][1], x_[1][1], x_[2][1]))
              ]

```

if not 与if没有区别，只是作为列表推导式的一个条件，以remove()方法的keyerror作为唯一值存在与否的标志，无论是if 还是 if not对此并无不同，if 、 if not只是对unique具有不同，前者导致[]
,后者导致唯一值的输出

if时：

if not时：
