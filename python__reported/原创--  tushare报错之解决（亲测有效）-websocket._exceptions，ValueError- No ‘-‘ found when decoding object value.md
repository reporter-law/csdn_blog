# 原创

： tushare报错之解决（亲测有效）：websocket._exceptions，ValueError: No ‘:‘ found when decoding object value

# tushare报错之解决（亲测有效）：websocket._exceptions，ValueError: No ‘:‘ found when decoding object value

### tushare报错：websocket._exceptions，ValueError: No ':' found when decoding object value

# 一、修改后结果

# 二、报错

第一个报错：

```
websocket._exceptions

```

具体含义是websocket中缺失_exceptions，

github上：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722090833520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
pip uninstall websocker
pip install websocket-client

```

无效

准确解决方法：换成1.2.50版本

第二个报错：

```
ValueError: No ':' found when decoding object value

```

格式解码不对

解决方法：

来源：链接: [tushare 之get_today_all修复接口完整code](https://blog.csdn.net/xsophiax/article/details/106613508).

```
text = text.replace('""', '"')

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722091138780.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722091159567.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

如上所述：无效

解决方法二：<br/> 出错的原因在于：新浪接口返回的数据已经修改了，原来的提取数据的方法就出现错误

准确解决方法：

将stock/trading.py源文件的_parsing_dayprice_json（）函数为：中的这些代码注释掉

```
#reg = re.compile(r',(.*?):')
#text = reg.sub(r',"\1":', text.decode('gbk') if ct.PY3 else text)
t#ext = text.replace('"{symbol', '{"symbol')
#text = text.replace('{symbol', '{"symbol"')
#if ct.PY3:
#jstr = json.dumps(text)
#else:
#jstr = json.dumps(text, encoding='GBK')
#js = json.loads(jstr)

```

换成

```
js = text.decode('utf8')  

```

# 三、成功获取

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722092410397.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200722092424197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
