# 原创

： python+keras汉字单字语音识别

# python+keras汉字单字语音识别

### python+keras单字语音识别

# 一、两种思路

就当前学习所知，有两种语音识别的思路<br/> 1、将语音文件提取mfcc，即转为二维张量形式，然后进行dense全连接层叠层训练，当然这个也可以使用传统机器学习方法。<br/>
转为二维张量格式为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129212209408.png"/><br/>
2、将语音文件提取mfcc转为三维张量形式即频谱图，然后进行cnn卷积神经网络训练，看了几个资料，这个似乎准确率更高，但是比较麻烦<br/> 所以下文采取第一种方式进行尝试<br/>
频谱图形式为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129215050314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、代码更新

采取第一种思路的代码为大佬南方朗郎：《python+keras实现语音识别》，这个代码有些小问题<br/> 1、keras版本问题<br/>
报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129213323603.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
准确的说，这个不是keras版本问题，应该是tensorflow版本的问题，tensorflow是keras的后端，我的python版本是3.8，所以安装的tensorflow版本是2.0以上的，而作者源码是建立在keras后端tensorflow1.0以上的版本，所以出现这样的错误，这样的错误会很多，一个个修改非常麻烦，但是python3.8好像没有支持的tensorflow1.0以上的版本，只有2.0以上的版本。<br/>
不过，幸运的是，我有两个python版本，一个3.7，一个3.8，python3.7有支持的tensorflow1.0以上的版本，于是我用python3.7安装了tensorflow1.15.5版本的tensorflow,<br/>
这个问题得以解决

2、代码有部分出现缺漏<br/>
报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129213936629.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这个报错是由于num_class没有传递过来，导致label标签one-hot化不成功<br/>
打印num_class时发现num_class=0，应该为2的<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129214202419.jpg"/>

将之传递过来<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129214254960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
模型正常训练<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129214313512.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是准确率不行，作者有提到似乎是因为数据本身的原因，有些数据存在问题<br/> 3、代码特征处理会报list index out of range<br/>
这一行<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129215307173.png"/><br/>
在作者跑的语音数据集上是不需要修改的，因为都是16000,但是跑自己的数据集就要修改，因为不一定是16000<br/>
修改为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210129215428736.png"/>

```
data.remove(0)

```

dense层模型调控最优的结果为测试集上93%左右<br/> 设置为：

```
	model = Sequential()
    model.add(Dense(1024, activation='relu'))
    model.add(Dropout(0.2))
    model.add(Dense(512, activation='relu'))
    model.add(Dense(256, activation='relu'))
    model.add(Dense(128, activation='relu'))

```

# 三、汉字语音识别

1、数据集问题<br/> 数据集使用的是百度语音合成对3500个常用汉字进行合成的数据集，每个字大概8个不同发音人，之后进行数据增强。<br/>
数据增强主要是对波形、位移以及加噪等处理，可以参见大佬凌逆战：《音频数据增强及python实现》链接: [音频数据增强及python实现](https://blog.csdn.net/qq_34218078/article/details/108907402?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=python%E9%9F%B3%E9%A2%91%E5%8A%A0%E5%99%AA&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-108907402.first_rank_v2_pc_rank_v29&amp;spm=1018.2226.3001.4187)
.

2、跑的结果<br/>
三个数据集，每个数据集有32个音频文件，一共96个，训练集85个，测试集15个，三分类样本数据平均，测试集结果1.0。<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210130083429672.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210130083448128.png"/><br/>
3、问题<br/> 这里的问题在于数据增强暂时只是用的音量，所以测试集与训练集可能没有什么差异，导致了这个结果，后续加噪、波形拉长等等后准确率可能会迅速下降。
