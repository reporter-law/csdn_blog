# 原创

： doc转为docx后不能打开，报错：docx.opc.exceptions.PackageNotFoundError: Package not found at

# doc转为docx后不能打开，报错：docx.opc.exceptions.PackageNotFoundError: Package not found at

### doc转为docx后不能打开，报错：docx.opc.exceptions.PackageNotFoundError: Package not found at

# 一、报错

```
docx.opc.exceptions.PackageNotFoundError: Package not found at

```

# 二、解决方法

## 1、参考博文

参照博文: [link](https://blog.csdn.net/smile_to_the_world/article/details/105090619).<br/>
此处需要说明，我的问题并不是他的“其实问题就出在最后一行的第二个参数16上，16代表的存储格式为doc，我应该改成12，12代表的是转存的格式为docx。修改成12后，python-docx就能读取文件了。”<br/>
而是原来转换是转为word,但是用的是wps

## 2、最值得注意的地方

原转换程序：

```
w = wc.Dispatch('Word.Application')  # 实例化

'''win32打开并保存而不能直接保存'''
doc = w.Documents.Open(path_)
doc.SaveAs(path_.split('.')[0] + ".docx", 16)  # 必须有参数16，否则会出错.

```

此处的path_是我自己传入的地址参数

先转换程序为

```
w = wc.gencache.EnsureDispatch('kwps.application')
doc = w.Documents.Open(path_)
doc.SaveAs2(path_.split('.')[0] + ".docx", 16)

```

比较：

```
#原程序
w = wc.Dispatch('Word.Application')
#先程序
w = wc.gencache.EnsureDispatch('kwps.application')

```

即读取不成功在于用wps读取转为word的文档，因为报错“docx.opc.exceptions.PackageNotFoundError: Package not found at”

总结：注意文件格式的问题，不仅包括后缀也包括使用的软件
