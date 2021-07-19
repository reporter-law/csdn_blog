# 原创

： Keras.Backend的一些理解

# Keras.Backend的一些理解

### Keras.Backend的一些理解（备份）

# 一、理解

我理解的深度学习层级由大到小为：Model&gt;layer&gt;函数，方法形成layer层，layer层形成model，keras.backend即后端，其实就是将深度学习向比layer更小的方法即函数下沉，更能实现灵活性；这里的方法即函数层，其实就是一些基本的数值处理方法，例如求均值的mean、求最大值的max，求点积的dot等，这些方法组合就可以形成一个layer,loss等基本的层。

# 二、重要的一些backend函数（方法）

```
import os, warnings
import keras.backend as K
"""placeholder()函数是在神经网络构建graph的时候在模型中的占位，此时并没有把要输入的数据传入模型，
它只会分配必要的内存。等建立session，在会话中，运行模型的时候通过feed_dict()函数向占位符喂入数据"""
inputs = K.placeholder(shape=(2, 4, 5))
# 同样可以：
inputs = K.placeholder(shape=(None, 4, 5))
# 同样可以：
inputs = K.placeholder(ndim=3)
"""==input，说明数据格式"""
print(inputs)
"""下面的代码实例化一个变量。它等价于 `tf.Variable()` 或 `th.shared()`。"""


import numpy as np
val = np.random.random((3, 4, 5))
var = K.variable(value=val)
print(var)
# 全 0 变量：
var = K.zeros(shape=(3, 4, 5))
# 全 1 变量：
var = K.ones(shape=(3, 4, 5))
"""区别：Tensor("Placeholder_2:0", shape=(?, ?, ?), dtype=float32)
&lt;tf.Variable 'Variable:0' shape=(3, 4, 5) dtype=float32_ref&gt;
&lt;tf.Variable 'Variable_2:0' shape=(3, 4, 5) dtype=float32_ref&gt;
tensor,h和"""



"""你需要的大多数张量操作都可以像在 TensorFlow 或 Theano 中那样完成：

```python"""
# 使用随机数初始化张量
b = K.random_uniform_variable(shape=(3, 4), low=0, high=1) # 均匀分布
c = K.random_normal_variable(shape=(3, 4), mean=0, scale=1) # 高斯分布
d = K.random_normal_variable(shape=(3, 4), mean=0, scale=1)
import  tensorflow as tf
inter_sess=tf.InteractiveSession()
tf.global_variables_initializer().run()
# 张量运算
a = b + c * K.abs(d)
print("b:",inter_sess.run(b))
print("c:",inter_sess.run(c))
print("d:",inter_sess.run(d))
print("a:",inter_sess.run(a))
#0.7-2*-0.2
c = K.dot(a, K.transpose(b))
print("transpose意义:")
print(inter_sess.run(b))
print(inter_sess.run(K.transpose(b)))


"""dot的意义"""
aqq = K.ones((1,1))
bqq = K.ones((1,2))
cqq = K.dot(aqq, bqq)
print(K.eval(aqq))
print(K.eval(bqq))
print(cqq.shape)
print(K.eval(cqq))
print("结论，没有加减，似乎只是行列的变换，值没有变换")

#print("下一个是求余弦相似度：余弦相似度就是相似程度，余弦相似度是而为空间中两个量接近程度，a^2*b^2=c^2,但是dot只是向量乘积")
print("c1:",inter_sess.run(c))
a = K.sum(b, axis=1)
print("sum:",inter_sess.run(a))

"""softmax"""
print("softmax的意义&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;")
a = K.softmax(b)
print(K.eval(b))
print("softmax:",inter_sess.run(a))
print("结论：肺腑，转一，即每个数的比重")

"""concate"""
print("concate的意义&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;")
a = K.concatenate([b, c], axis=-1)
print("b:",K.eval(b))
print("c:",K.eval(c))
print("a3:",K.eval(a))
print(a)
print("结论，行值增加，但不是值相加而是行特征增加")
# 等等


"""numpy转keras Numpy 数组转换为默认的 Keras 浮点类型"""

print(K.floatx())
'float32'
arr = np.array([1.0, 2.0], dtype='float64')
print(arr.dtype)
"""dtype('float64')"""
new_arr = K.cast_to_floatx(arr)
print(new_arr)
'array([ 1.,  2.], dtype=float32)'
print(new_arr.dtype)

var1 = np.array([1.0,2.0],dtype='float64')
print(var1)
var2 = np.array([1.0,1.0],dtype='float64')
print(var2)
new_var1 = K.cast_to_floatx(var1)
new_var2 = K.cast_to_floatx(var2)
print(new_var1.dtype)


"""to_dense,压缩张量"""

"""variable



keras.backend.variable(value, dtype=None, name=None, constraint=None)

实例化一个变量并返回它。"""
val1 = np.array([[3,3],
                 [5,5]])
kvar1 = K.variable(value=val1, dtype='float64', name='example_var')
val2 = np.array([[4, 4],
                 [8,8]])
kvar2 = K.variable(value=val2, dtype='float64', name='example_var1')
print(val1,val2)
print(K.eval(K.dot(kvar1,kvar2)))
print("dot:的作用为:3*4+3*8=36,36,60,60")

"""constant"""
print(K.eval(K.constant(value=[1.2,1.3])))
"""&gt;&gt;&gt;&gt;非变量，即b"""

"""返回函数：ndim==轴即维度，eval==值"""

"""单位矩阵"""
print(K.eval(K.eye(3)))

"""count_params:数组中静态维度的乘积"""
kvar = K.zeros((21,10))
print(K.count_params(kvar))



"""### dot
python
keras.backend.dot(x, y)



将 2 个张量（和/或变量）相乘并返回一个*张量*。"""

"""
prod

keras.backend.prod(x, axis=None, keepdims=False)
在某一指定轴，计算张量中的值的乘积。

"""

"""
### concatenate

keras.backend.concatenate(tensors, axis=-1)


基于指定的轴，连接张量的列表。

__参数__

- __tensors__: 需要连接的张量列表。
- __axis__: 连接的轴。

__返回__

一个张量。

----
"""
""" reshape

keras.backend.reshape(x, shape)

将张量重塑为指定的尺寸。

__参数__

- __x__: 张量或变量。
- __shape__: 目标尺寸元组。

__返回__

一个张量。
"""
""" permute_dimensions

keras.backend.permute_dimensions(x, pattern)
重新排列张量的轴。
"""

print("前：",K.eval(K.eye(2)))
kvar_tile = K.tile(K.eye(2), (2, 2))
print("后：",K.eval(kvar_tile))
print("结论，后面的2是复制特征，前面的是复制维度")

"""stack"""
print("前：",K.eval(K.ones((3,3,3))))
A = K.stack(K.ones((3,3,3)), axis=0)
print("后：",K.eval(A))
print("结论为：")

""""""
### repeat_elements
print("前：",K.eval(K.eye(3)))
print(K.eval(K.repeat_elements(K.eye(3), 3, 1)))#axis=0为竖轴，axis为1为横轴


"""### get_value

keras.backend.get_value(x)
返回一个变量的值。
__参数__

- __x__: 输入变量。

__返回__

一个 Numpy 数组。
"""
print("前：",K.eval(K.eye(3)))
print(K.get_value(K.eye(3)),type(K.get_value(K.eye(3))))
print("结论：keras格式转为numpy")
"""
 print_tensor
keras.backend.print_tensor(x, message='')
"""
print(K.eval(K.eye(2)))
print(K.print_tensor(K.eye(2)))
print("变成tensor")

"""
### categorical_crossentropy

keras.backend.categorical_crossentropy(target, output, from_logits=False)
"""
print("前",K.eval(K.ones((3,3))),K.eval(K.eye(3)))
print()
print("分类交叉烱：",K.eval(K.categorical_crossentropy(K.ones((3,3)),K.eye(3))))
print("gradients")
varqq =[K.zeros((3,3)),K.ones((3,3)),K.ones((3,3))]
loss = K.categorical_crossentropy(varqq,K.eye(3))
print(K.gradients(loss, var))

```
