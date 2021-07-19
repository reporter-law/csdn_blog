# 原创

： 利用pandas进行exceld 的列相加求和

# 利用pandas进行exceld 的列相加求和

### 利用pandas进行exceld 的列相加求和

# 一、简单的列相加

```
dataframe["新列“]=dataframe["第一列”]+dataframe["第二列“]

```

# 二、多列相加

对于多列相加或者不知道列名只知道索引的，用上面简单的方法相加就会比较麻烦<br/> 方法：找出自己需要的相加的列的索引，然后进行循环<br/>
此处我需要第三列之后的进行相加<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200703223307385.png"/><br/>
一共46列，一个一个写列名比较麻烦，通过numpy的sum方法进行相加

```
for i in range(3,df.shape[1]):
    list_.append(df.iloc[:, i])
df["汇总"] = np.sum(list_, axis = 0)

```

最后结果
