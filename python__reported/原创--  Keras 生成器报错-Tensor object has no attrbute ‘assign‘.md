# 原创

： Keras 生成器报错:Tensor object has no attrbute ‘assign‘

# Keras 生成器报错:Tensor object has no attrbute ‘assign‘

### Tensor has no attrbute assign

# 一、keras生成器重心

我是在使用keras生成器时出现了这个报错并引发后续一系列报错<br/> keras生成器使用的是studyer_domi：《2020-12-11 keras通过model.fit_generator训练模型(节省内存)
》链接: [l2020-12-11 keras通过model.fit_generator训练模型(节省内存)](https://blog.csdn.net/qingfengxd1/article/details/111032641?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161224282016780271566001%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&amp;request_id=161224282016780271566001&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v29-1-111032641.pc_search_result_before_js&amp;utm_term=2020-12-11keras%E7%94%9F%E6%88%90%E5%99%A8&amp;spm=1018.2226.3001.4187)
.

其实根本不用管yield的问题，生成器就是起到连续调用函数，可以遍历return结果的方式。<br/> 因而keras生成器处重点反而在于keras网络配置上的不一样的地方

# 二、keras生成器

```
def data_generate(lis):
    count=1
    batch_size = 10
    while 1:
        batch_x = [x[0] for x in lis[(count - 1) * batch_size:count * batch_size]]
        batch_y = [y[1] for y in lis[(count - 1) * batch_size:count * batch_size]]
        batch_x = np.array([np.asarray(get_wav_mfcc(i)) for i in batch_x])
        batch_y =np.array(batch_y)
        count = count + 1
        yield batch_x, batch_y
"""lis的形状为[["xxx.wav",[0. 1. 0. 0. 0.]],
						["sss.wav",[0. 0. 1. 0. 0.]],
						["zzz.wav",[0. 0. 0. 0. 1.]],]
						这样二维张量形式"""
	#其中“xxx.wav”等就是需要处理文件的路径，我的是音频文件，如上所述，get_wav_mfcc(i)对音频进行读取并返回数值型的数据
	#而[0. 1. 0. 0. 0.]是已经编码好的one-hot标签
	#两个格式都是numpy.array

```

具体格式如下：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2021020213271758.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 三、报错

在此处记录遇到的报错，这些报告基本与keras有关，也是我之前在model.fit()中没有修改过来的地方

报错一：

```
ValueError: Please provide as model inputs either a single array or a list of arrays. You passed: x=&lt;generator object data_generate at 0x0000028725967D68&gt;

```

```
这是由于model.fit()没有修改为model.fit_generator()

```

报错二：

```
RuntimeError: You must compile your model before using it.

```

这是由于没有设置input_shape,但是在model.fit()中不用设置这一参数也可训练<br/> 应该修改为：

```
model = Sequential()
model.add(Dense(2048, activation='relu',input_shape=(32000,)))

```

第三个报错：

```
Tensor object has no attrbute 'assign'

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210202133834945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
将

```
model.add(Dense(num_class, activation='softmax'))

```

修改为

```
model.add(Dense(11, activation='softmax'))

```

11是我自己标签种类，需要按自己的标签种类设置

tf.assign是变量替换，tf.assign(x,new_x) 等价于x = new_x

上述修改完成后就可以训练了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210202134521899.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
