# 原创

： python《深度学习》keras基本理解

# python《深度学习》keras基本理解

### python《深度学习》keras初步理解

# 一、Sequential()

```
from keras import models#构架模型
from keras import layers#神经网络层
from keras.datasets import imdb
#其中imdb是电影评论数据集，但是被处理过，	已被编码过了，所以只有index,而没有实际内容，需要进行转化

model = models.Sequential()#网络结构决定了假设空间，这是线性堆叠方式

```

线性堆叠方式也即序贯模型是神经网络的构架，即神经网络的层与层之间是怎么连接的。<br/> Sequential()
是按照线性方式，可以理解为流水线作业方式。结合这个可视化网站理解: [神经网络游乐场](http://playground.tensorflow.org/#activation=relu&amp;batchSize=10&amp;dataset=xor&amp;regDataset=reg-plane&amp;learningRate=0.00001&amp;regularizationRate=0&amp;noise=0&amp;networkShape=3,2&amp;seed=0.34603&amp;showTestData=false&amp;discretize=false&amp;percTrainData=50&amp;x=true&amp;y=true&amp;xTimesY=true&amp;xSquared=true&amp;ySquared=true&amp;cosX=false&amp;sinX=true&amp;cosY=false&amp;sinY=true&amp;collectStats=false&amp;problem=classification&amp;initZero=false&amp;hideText=false)
.

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210106175953757.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这是一个输入到输出的整个过程实现线状的流动过程，上层处理完毕交给下层继续处理。<br/> 要叠多少层就直接用model.add即可

# 二、层与神经元

```
model.add(layers.Dense(32,input_shape=(784,)))#32是维度即输出多少个结果即神经	网络的层数即次数，input_shape是输入数据的大小，一次多少样本数量不在这里！！而是batch_size
model.add(layers.Dense(32))

```

Dense为keras的一个神经网络层，层就相当于一个环节，想象为流水线作业，每一层就是一个流水线的环节，在可视化的图中可以表示为这一个圆圈整体涵盖的所有<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2021010617575598.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这是一个神经元的三层<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210106181432532.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这是两个神经元的三层结构

其中dense是全连接层，处理2d张量（向量），即呈现为<br/> [[1,2,3],<br/> [2,3,4],<br/> [3,4,5]]<br/> 这样结构的数据，此外还有<br/>
3d张量用循环层lstm层；4d张量用二维卷积层（conv2d层）

而神经元就是model.add(layers.Dense(32,input_shape=(784,)))中32所决定的内容，32表示由32个神经元。<br/>
在可视化图中为一个个方框<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210106180741768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这是三层，每层一个神经元

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210106180857642.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这是三层，每层两个神经元

神经元数量由Dense的第一个参数控制，可以自由选择<br/> 其中输入数据的格式在,input_shape中设置，,input_shape=(784,)可以看成是一个含有784个数值的列表
