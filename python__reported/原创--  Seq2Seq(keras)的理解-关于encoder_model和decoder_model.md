# 原创

： Seq2Seq(keras)的理解：关于encoder_model和decoder_model

# Seq2Seq(keras)的理解：关于encoder_model和decoder_model

### Seq2Seq_keras:关于encoder_model和decoder_model

# 一、三个model

## （一）Seq2Seq之前的keras model:

### 1、创建模型

```
# 多层感知机(MLP)模型
from keras.models import Model
from keras.layers import Input, Dense
from keras.utils import plot_model

mnist_input = Input(shape=(784,), name='input')
hidden1 = Dense(512, activation='relu', name='hidden1')(mnist_input)
hidden2 = Dense(216, activation='relu', name='hidden2')(hidden1)
hidden3 = Dense(128, activation='relu', name='hidden3')(hidden2)
output = Dense(10, activation='softmax', name='output')(hidden3)

model = Model(inputs=mnist_input, outputs=output)

# 打印网络结构
model.summary()
model.save(r"xxx.h5")
# 產生網絡拓撲圖
plot_model(model, to_file='模型.png')

```

### 2、模型预测

```
model = load_model(r"xxx.h5")
model.predict()

```

## （二）Seq2Seq的keras model

完整代码链接: [十分钟介绍 Keras 中的序列到序列学习](https://blog.keras.io/a-ten-minute-introduction-to-sequence-to-sequence-learning-in-keras.html).<br/>
此处会有三个模型需要进行保存

```
1.训练模型：
from keras.models import Model
from keras.layers import Input, LSTM, Dense

# Define an input sequence and process it.
encoder_inputs = Input(shape=(None, num_encoder_tokens))
encoder = LSTM(latent_dim, return_state=True)
encoder_outputs, state_h, state_c = encoder(encoder_inputs)
# We discard `encoder_outputs` and only keep the states.
encoder_states = [state_h, state_c]

# Set up the decoder, using `encoder_states` as initial state.
decoder_inputs = Input(shape=(None, num_decoder_tokens))
# We set up our decoder to return full output sequences,
# and to return internal states as well. We don't use the 
# return states in the training model, but we will use them in inference.
decoder_lstm = LSTM(latent_dim, return_sequences=True, return_state=True)
decoder_outputs, _, _ = decoder_lstm(decoder_inputs,
                                     initial_state=encoder_states)
decoder_dense = Dense(num_decoder_tokens, activation='softmax')
decoder_outputs = decoder_dense(decoder_outputs)

# Define the model that will turn
# `encoder_input_data` &amp; `decoder_input_data` into `decoder_target_data`
model = Model([encoder_inputs, decoder_inputs], decoder_outputs)



2.推理模型
2.1编码模型
encoder_model = Model(encoder_inputs, encoder_states)
2.2解码模型
decoder_state_input_h = Input(shape=(latent_dim,))
decoder_state_input_c = Input(shape=(latent_dim,))
decoder_states_inputs = [decoder_state_input_h, decoder_state_input_c]
decoder_outputs, state_h, state_c = decoder_lstm(
    decoder_inputs, initial_state=decoder_states_inputs)
decoder_states = [state_h, state_c]
decoder_outputs = decoder_dense(decoder_outputs)
decoder_model = Model(
    [decoder_inputs] + decoder_states_inputs,
    [decoder_outputs] + decoder_states)

```

总共三个模型！！！！！<br/> 初见，抓狂！！！<br/> 里面的lstm，state_h, state_c已经特别难理解了，后面还要三个模型，于是放弃治疗了。

# 二、再次遇见seq2seq

理解seq2seq有几个难点

## 难点一：lstm

通过可视化的操作理解了lstm<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210703090619960.gif"/>

可视化的理解链接: [LSTM这一篇就够了](https://blog.csdn.net/yingqubaifumei/article/details/100888147?spm=1001.2014.3001.5506).

## 难点二：return_sequences和return_state

return_sequences:即返回序列，若为True，则返回每一个序列<br/> 要理解这一点，首先要明白rnn的基本原理

```
以自然语言处理为例：
1、我们的输入通常为字符级即一个一个字输入rnn中，
正常来说每个输入就有一个输出。
2、但是在文本分类或者情感分类中，
我们得到的结果为几个类别，如积极、消极，
从字符上来说明显不对应
3、这就是因为return_sequences=False的结果，
因为RNN会将预测的每个输入作为下一个输入的一起进行输入，
即输入为[y（上一个x的输出),x(当前输入）]
如下图：

```

```
return_sequences=True
就是每个时间步也就是每个x的y都输出来
如下文实验所展示的：

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210703091930973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210703091955978.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210703092016476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
而return_state则为计算每一个时间步的y即return_sequences的计算方式
如下文实验

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20210703092242380.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2021070309225842.png"/>

```
这两个就决定了state_h, state_c的出现与否，
即return_sequences=state_h,return_state=state_c

```

综上我的理解就是，每个输入的x以某种计算方式计算出每个y,每个以某种方式计算出最终的y.<br/> 即f(f(x))=y

state_h,state_c就是提取计算最终y的f()，将编码器中的f()找出来然后作为解码器的初始参数，然后解码，实现可变长度序列。

## 难点三：三个模型

```
本质：三个模型本质上时一个模型
我重新修改了一下代码写的方式：
"""设计模型"""
def creat_model():
    # 定义输入的序列
    # 注意：因为输入序列长度(timesteps)可变的情况，使用input_shape =（None，num_features）
    encoder_inputs = Input(shape=(None, num_encoder_tokens), name='encoder_input')
    """后为特征数，前为批次数量！！！"""
    encoder = LSTM(latent_dim, return_state=True, name='encoder_lstm')  # 需要取得LSTM的内部state, 因此设定"return_state=True"
    encoder_outputs, state_h, state_c = encoder(encoder_inputs)
    """输出，输入最后一个状态(和前一个是一样的相当于下一轮输入的x)，隐藏计算f"""
    # 我们抛弃掉`encoder_outputs`因为我们只需要LSTM cell的内部state参数
    encoder_states = [state_h, state_c]

    ###############解码器是一个模型，编码器只是解码器模型的前期数据处理！！！！！！！！！
    # ==== 解码 (decoder) ====

    # 设定解码器(decoder)
    # 注意：因为输出序列的长度(timesteps)是变动的，使用input_shape =（None，num_features）
    decoder_inputs = Input(shape=(None, num_decoder_tokens), name='decoder_input')

    # 我们设定我们的解码器回传整个输出的序列同时也回传内部的states参数
    decoder_lstm = LSTM(latent_dim, return_sequences=True, return_state=True, name='decoder_lstm')

    # 在训练时我们不会使用这些回传的解码的states, 但是在预测时我们会用到这些解码器states参数？？？？？
    # **解码器的初始状态是使用编码器的最后的状态(states)**
    decoder_outputs, _, _ = decoder_lstm(decoder_inputs,
                                         initial_state=encoder_states)  # 我们使用`encoder_states`来做为初始值(initial state) &lt;-- 重要

    # 接密集层(dense)来进行softmax运算每一个字符可能的机率
    decoder_dense = Dense(num_decoder_tokens, activation='softmax', name='decoder_output')
    decoder_outputs = decoder_dense(decoder_outputs)

    # 定义一个模型接收encoder_input_data` &amp; `decoder_input_data`做为输入而输出`decoder_target_data`
    model = Model([encoder_inputs, decoder_inputs], decoder_outputs)

    # 打印出模型结构
    #model.summary()
    # from keras.utils import plot_model
    # 拓扑图
    # plot_model(model, to_file='seq2seq_graph.png')
    return model
"""这就是最开始的那个训练模型"""

#其余两个模型只是对这个模型参数的提取
model = creat_model()
# 设定模型超参数
model.compile(optimizer=Adam(), loss='categorical_crossentropy', metrics=["accuracy"])

# 开始训练
model.fit([encoder_input_data, decoder_input_data], decoder_target_data,
          batch_size=256,
          epochs=2,
          validation_split=0.2)
model.save('model\s2s1.h5')

"""预测时"""
for layer in model.layers:
    if layer.name =="encoder_lstm":
        print(layer.name)
        encoder_lstm = layer
        encoder_inputs = Input(shape=(None, num_encoder_tokens), name='encoder_input')
        encoder_outputs, state_h, state_c = encoder_lstm(encoder_inputs)
        encoder_states = [state_h, state_c]
        encoder_model = Model(encoder_inputs, encoder_states)
    elif layer.name == "decoder_lstm" :
        decoder_lstm = layer
    elif layer.name == "decoder_output":
        decoder_dense = layer

        decoder_inputs = Input(shape=(None, num_decoder_tokens), name='decoder_input')
        decoder_state_input_h = Input(shape=(latent_dim,))
        decoder_state_input_c = Input(shape=(latent_dim,))
        decoder_states_inputs = [decoder_state_input_h, decoder_state_input_c]

        # # 解码器(decoder)定义初始状态(initial decoder state)
        """用上_,_"""
        decoder_outputs, state_h, state_c = decoder_lstm(
            decoder_inputs, initial_state=decoder_states_inputs)  # 我们使用`decoder_states_inputs`来做为初始值(initial state)

        decoder_states = [state_h, state_c]
        decoder_outputs = decoder_dense(decoder_outputs)

        # 定义解码器(decoder)的模型
        decoder_model = Model([decoder_inputs] + decoder_states_inputs, [decoder_outputs] + decoder_states)

```

# 三、seq2seq全部代码

```
import  warnings
from keras.optimizers import Adam
from keras.models import load_model
warnings.filterwarnings("ignore")
from  keras.models import  Model
from  keras.layers  import  Input,LSTM,Dense
import  numpy  as  np
import  os

#专案的根目录路径
ROOT_DIR  =  os.getcwd ()

#置放训练数据的目录
DATA_PATH  =  os.path.join ( ROOT_DIR,"data" )

#训练数据档
DATA_FILE  =  os.path.join ( DATA_PATH , "cmn-tw.txt" )

batch_size  =  32  #训练时的批次数量
epochs  =  100  #训练循环数
latent_dim  =  128  #编码后的潜在空间的维度(dimensions of latent space)
num_samples  =  10000  #用来训练的样本数

"""数据向量化"""
input_texts = []
target_texts = []
input_characters = set()  # 英文字符集
target_characters = set()  # 中文字符集
lines = open(DATA_FILE, mode="r", encoding="utf-8").read().split('\n')

# 逐行的读取与处理
for line in lines[:min(num_samples, len(lines) - 1)]:
    input_text, target_text = line.split('\t')

    # 我们使用“tab”作为“开始序列[SOS]”字符或目标，“\n”作为“结束序列[ EOS]”字符。&lt;-- **重要
    target_text = '\t' + target_text + '\n'

    input_texts.append(input_text)
    target_texts.append(target_text)

    for char in input_text:
        if char not in input_characters:
            input_characters.add(char)
    for char in target_text:
        if char not in target_characters:
            target_characters.add(char)

input_characters = sorted(list(input_characters))  # 全部输入的字符集
target_characters = sorted(list(target_characters))  # 全部目标字符集

num_encoder_tokens = len(input_characters)  # 所有输入字符的数量
num_decoder_tokens = len(target_characters)  # 所有输目标字符的数量

max_encoder_seq_length = max([len(txt) for txt in input_texts])  # 最长的输入句子长度
max_decoder_seq_length = max([len(txt) for txt in target_texts])  # 最长的目标句子长度

"""基本信息"""
print('Number of samples:', len(input_texts))
print('Number of unique input tokens:', num_encoder_tokens)
print('Number of unique output tokens:', num_decoder_tokens)
print('Max sequence length for inputs:', max_encoder_seq_length)
print('Max sequence length for outputs:', max_decoder_seq_length)

# 输入字符的索引字典
input_token_index = dict(
    [(char, i) for i, char in enumerate(input_characters)])

# 输目标字符的索引字典
target_token_index = dict(
    [(char, i) for i, char in enumerate(target_characters)])

# 包含英文句子的one-hot向量化的三维形状数组（num_pairs，max_english_sentence_length，num_english_characters）
encoder_input_data = np.zeros(
    (len(input_texts), max_encoder_seq_length, num_encoder_tokens),
    dtype='float32')

# 包含中文句子的one-hot向量化的三维形状数组（num_pairs，max_chinese_sentence_length，num_chinese_characters）
decoder_input_data = np.zeros(
    (len(input_texts), max_decoder_seq_length, num_decoder_tokens),
    dtype='float32')

# decoder_target_data与decoder_input_data相同，但是偏移了一个时间步长。
# decoder_target_data [:, t，：]将与decoder_input_data [：，t + 1，：]相同
decoder_target_data = np.zeros(
    (len(input_texts), max_decoder_seq_length, num_decoder_tokens),
    dtype='float32')

# 把数据转换成要用来训练用的张量数据结构&lt;--重要
for i, (input_text, target_text) in enumerate(zip(input_texts, target_texts)):
    for t, char in enumerate(input_text):
        encoder_input_data[i, t, input_token_index[char]] = 1.
        """在全零向量中找出为1的向量，这些即为索引"""

    for t, char in enumerate(target_text):
        # decoder_target_data 比decoder_input_data 领先一个时间步??????????
        """推断下一个字？？？？？？？？？？"""
        decoder_input_data[i, t, target_token_index[char]] = 1.
        if t &gt; 0:
            # decoder_target_data will be ahead by one timestep
            # and will not include the start character.
            decoder_target_data[i, t - 1, target_token_index[char]] = 1.


"""设计模型"""
def creat_model():
    # 定义输入的序列
    # 注意：因为输入序列长度(timesteps)可变的情况，使用input_shape =（None，num_features）
    encoder_inputs = Input(shape=(None, num_encoder_tokens), name='encoder_input')
    """后为特征数，前为批次数量！！！"""
    encoder = LSTM(latent_dim, return_state=True, name='encoder_lstm')  # 需要取得LSTM的内部state, 因此设定"return_state=True"
    encoder_outputs, state_h, state_c = encoder(encoder_inputs)
    """输出，输入最后一个状态(和前一个是一样的相当于下一轮输入的x)，隐藏计算f"""
    # 我们抛弃掉`encoder_outputs`因为我们只需要LSTM cell的内部state参数
    encoder_states = [state_h, state_c]

    ###############解码器是一个模型，编码器只是解码器模型的前期数据处理！！！！！！！！！
    # ==== 解码 (decoder) ====

    # 设定解码器(decoder)
    # 注意：因为输出序列的长度(timesteps)是变动的，使用input_shape =（None，num_features）
    decoder_inputs = Input(shape=(None, num_decoder_tokens), name='decoder_input')

    # 我们设定我们的解码器回传整个输出的序列同时也回传内部的states参数
    decoder_lstm = LSTM(latent_dim, return_sequences=True, return_state=True, name='decoder_lstm')

    # 在训练时我们不会使用这些回传的解码的states, 但是在预测时我们会用到这些解码器states参数？？？？？
    # **解码器的初始状态是使用编码器的最后的状态(states)**
    decoder_outputs, _, _ = decoder_lstm(decoder_inputs,
                                         initial_state=encoder_states)  # 我们使用`encoder_states`来做为初始值(initial state) &lt;-- 重要

    # 接密集层(dense)来进行softmax运算每一个字符可能的机率
    decoder_dense = Dense(num_decoder_tokens, activation='softmax', name='decoder_output')
    decoder_outputs = decoder_dense(decoder_outputs)

    # 定义一个模型接收encoder_input_data` &amp; `decoder_input_data`做为输入而输出`decoder_target_data`
    model = Model([encoder_inputs, decoder_inputs], decoder_outputs)

    # 打印出模型结构
    #model.summary()
    # from keras.utils import plot_model
    # 拓扑图
    # plot_model(model, to_file='seq2seq_graph.png')
    return model
#model,encoder_model,decoder_model=creat_model()
if os.path.exists(r"model\s2s.h5"):

    model = load_model(r"model\s2s.h5")
    model.summary()
else:
    model = creat_model()
model = creat_model()
# 设定模型超参数
model.compile(optimizer=Adam(), loss='categorical_crossentropy', metrics=["accuracy"])

# 开始训练
model.fit([encoder_input_data, decoder_input_data], decoder_target_data,
          batch_size=256,
          epochs=2,
          validation_split=0.2)
model.save('model\s2s1.h5')
for layer in model.layers:
    if layer.name =="encoder_lstm":
        print(layer.name)
        encoder_lstm = layer
        encoder_inputs = Input(shape=(None, num_encoder_tokens), name='encoder_input')
        encoder_outputs, state_h, state_c = encoder_lstm(encoder_inputs)
        encoder_states = [state_h, state_c]
        encoder_model = Model(encoder_inputs, encoder_states)
    elif layer.name == "decoder_lstm" :
        decoder_lstm = layer
    elif layer.name == "decoder_output":
        decoder_dense = layer

        decoder_inputs = Input(shape=(None, num_decoder_tokens), name='decoder_input')
        decoder_state_input_h = Input(shape=(latent_dim,))
        decoder_state_input_c = Input(shape=(latent_dim,))
        decoder_states_inputs = [decoder_state_input_h, decoder_state_input_c]

        # # 解码器(decoder)定义初始状态(initial decoder state)
        """用上_,_"""
        decoder_outputs, state_h, state_c = decoder_lstm(
            decoder_inputs, initial_state=decoder_states_inputs)  # 我们使用`decoder_states_inputs`来做为初始值(initial state)

        decoder_states = [state_h, state_c]
        decoder_outputs = decoder_dense(decoder_outputs)

        # 定义解码器(decoder)的模型
        decoder_model = Model([decoder_inputs] + decoder_states_inputs, [decoder_outputs] + decoder_states)

reverse_input_char_index = dict(
    (i, char) for char, i in input_token_index.items())

reverse_target_char_index = dict(
    (i, char) for char, i in target_token_index.items())

# 对序列进行解码
def decode_sequence(input_seq):
    # 将输入编码成为state向量中间语义向量
    states_value = encoder_model.predict(input_seq)

    # 产生长度为1的空白目标序列
    target_seq = np.zeros((1, 1, num_decoder_tokens))

    # 添加特定的目标序列起始字符"[SOS]",在这个范例中是使用 "\t"字符，为什么要增加起始符，不是训练中有吗？？？？？
    #因为输入的数据没有起始符？？？？
    target_seq[0, 0, target_token_index['\t']] = 1.

    # 对批次的序列进行抽样
    stop_condition = False
    decoded_sentence = ''
    while not stop_condition:
        """解码器是新模型！！！！"""
        output_tokens, h, c = decoder_model.predict(
            [target_seq] + states_value)

        # 对标签抽样，一个一个预测
        sampled_token_index = np.argmax(output_tokens[0, -1, :])
        sampled_char = reverse_target_char_index[sampled_token_index]
        decoded_sentence += sampled_char

        # 停止循环的条件: 到达最大的长度或是找到"停止[EOS]"字符,在这个范例中是使用 "\n"字符
        if (sampled_char == '\n' or
                len(decoded_sentence) &gt; max_decoder_seq_length):
            stop_condition = True

        # 更新目标序列(of length 1).
        target_seq = np.zeros((1, 1, num_decoder_tokens))
        target_seq[0, 0, sampled_token_index] = 1.

        # 更新 states
        states_value = [h, c]

    return decoded_sentence


for seq_index in range(100):
    # 从训练集中取出一个序列并试著解码
    input_seq = encoder_input_data[seq_index: seq_index + 1]
    decoded_sentence = decode_sequence(input_seq)
    print('-')
    print('Input sentence:', input_texts[seq_index])
    print('Decoded sentence:', decoded_sentence)

```

参考文章：<br/> 《Keras中return_sequences和return_state有什么用？》 - 知乎<br/>
链接: [Keras中return_sequences和return_state有什么用？](https://zhuanlan.zhihu.com/p/85910281).<br/> 《LSTM神经网络输入输出究竟是怎样的？》 -
知乎<br/>
链接: [LSTM神经网络输入输出究竟是怎样的？](https://www.zhihu.com/tardis/landing/360/ans/318771336?query=LSTM%E7%A5%9E%E7%BB%8F%E7%BD%91%E7%BB%9C%E8%BE%93%E5%85%A5%E8%BE%93%E5%87%BA%E7%A9%B6%E7%AB%9F%E6%98%AF%E6%80%8E%E6%A0%B7%E7%9A%84%EF%BC%9F&amp;mid=52e2ccbd5e01bcebdadc63cb11ea5a36&amp;guid=233F410726DA5B3A1003DDA2D856697C.1624700609304)
.
