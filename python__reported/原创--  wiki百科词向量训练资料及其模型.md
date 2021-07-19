# 原创

： wiki百科词向量训练资料及其模型

# wiki百科词向量训练资料及其模型

### wiki百科词向量训练模型

# 一、结果预览

目标为求取python相关的内容为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808131831224.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808131913780.png"/><br/>
从结果上看，与python相关的内容为java、perl等编程语言

# 二、作用

个人简单理解：就是寻找相关的词，如上面的oython是一种编程语言，而perl、java等也是如此，但是又不是近义词，比如bash，bash是linux的命令处理器。

扩展用途：通过相关联的词进行分类、推荐（如广告推荐）、比较相似度等等；（个人觉得就是一个fuzzywuzzy更精确的版本）

理解可能不是很准确，可以参见以下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808133217485.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

关于其技术原理，可以参见链接: [全面理解word2vec](https://zhuanlan.zhihu.com/p/33799633).

# 训练过程

参见：: [《使用中文维基百科语料库训练一个word2vec模型》](https://blog.csdn.net/sinat_29957455/article/details/81432846?utm_source=blogxgwz8&amp;utm_medium=distribute.pc_relevant.none-task-blog-title-3&amp;spm=1001.2101.3001.4242).<br/>
模型基本上也是参照这篇文章训练出来的，

## （一）下载问题解决

只是相关工具下载过于困难，wiki资源最新的20200801的有2G左右，直接网页下载特别缓慢，换成迅雷只能享受几十秒的快速，接着也是几十kb的速度。

### 下载方式一：

首先下载idm，<br/>
就是这个<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808135446312.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

然后将网址导入idm

这个下载速度快点，大致在1mb左右

### 下载方式二：

使用闪电下载

<img alt="" src="https://img-blog.csdnimg.cn/2020080813562978.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
下载速度大致也在1mb左右

### 下载方式三：

我将资源以及训练的模型放在了天翼云盘中，下载速度平均在8M左右，最快能有十几M，

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020080814064665.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808140657576.png"/>

但是麻烦的是需要注册<br/> 下载链接： [模型以及资源](https://cloud.189.cn/t/aqIRnmiUnmay).

## （二）训练过程的问题

训练时长在40多分钟左右，我的计算机比较老了，更好的计算机能更快点<br/>
1、训练时设置的一个参数，min_count=1，默认为5，这应该实在计算词语的频数，默认为5，即小于5的可能是被省略了，因而设为1可能更好，当然这取决于个人训练的模型的用途

```
def main():
print("开始....................")
start_time = time.time()
#logging.basicConfig(format="%(asctime)s:%(levelname)s:%(message)s", level=logging.INFO)
sentences = word2vec.LineSentence(r"---.txt".strip('\u202a'))
model = word2vec.Word2Vec(sentences, size=250,min_count=1)
# 保存模型
model.save(r"law1.model".strip('\u202a'))
end = time.time()
across = (end-start_time)/60
print(across)

```

2、训练时可能遇到报错

```
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xba in position 0: invalid start byte

```

这个报错的原因不明，因为预训练的内容就是utf-8写入的（不是wiki数据，而是另一个训练的模型中遇到这个报错）

解决方式就是另存一份utf-8的文件

3、模型预测时的问题<br/> 可能遇到KeyError:

```
KeyError: "word 'python' not in vocabulary"

```

在我训练的另一个模型中，对python进行模型预测，发现了这个问题。当然在wiki模型中，如果预测内容为：

```
["腾讯","阿里巴巴"]

```

也会出现这种报错：

```
	KeyError: "word '腾' not in vocabulary" 或者 	KeyError: "word '阿' not in vocabulary"

```

这是训练时某些字被去掉了，”腾“字不明白为什么，但是”阿“字可能在停用词处理就去掉了，因而训练时会出现一定的失误

解决方法，就是将该词训练进去

```
def solution_keyerror():
"""对模型更新"""
sentences = [["腾讯","腾讯","腾讯","腾讯","腾讯","腾讯","腾讯","腾讯","腾讯","腾讯","腾讯" ]]

model = word2vec.Word2Vec.load('J:\PyCharm项目\项目\中国裁判文书网\word2ver裁判文书词向量\law.model')
print(model)
model.build_vocab(sentences, update=True)  # prepare the model vocabulary
model.train(sentences, total_examples=model.corpus_count, epochs=model.iter)
print(model.most_similar("腾讯", topn=20))

solution_keyerror()

```

结果为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200808142547304.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

这个方法并不是我想到的，而是来源于链接: [KeyError: “word ‘在行’ not in vocabulary”](https://blog.csdn.net/weixin_40143316/article/details/96463223?utm_medium=distribute.pc_relevant.none-task-blog-utm_term-1&amp;spm=1001.2101.3001.4242)
.
