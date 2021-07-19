# 原创

： text-cnn裁判文书分类

# text-cnn裁判文书分类

### text-cnn裁判文书分类

# 一、数据集

使用爬虫获取的26万份裁判文书，可以在链接:<br/> 链接: [全国范围内爬取的26万份裁判文书](https://pan.baidu.com/s/1MpBKQeF_nz0E1a_YcTv1vg).提取码：t2nh<br/>
训练模型源自链接: [Text Classification with CNN and RNN](https://github.com/gaussic/text-classification-cnn-rnn).

# 二、训练过程

一共训练5轮<br/>
数据格式为目录：标签名，文本为内容<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829215442293.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70#pic_center"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829215504909.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70#pic_center"/><br/>
写入方法

```
def wenshu_cut():
	with open(r"J:\PyCharm项目\github项目\文本分类\罪名分类\罪名分类.json", "r")as f:
    	train_text = {}
    	global one
    	text = f.read()
    	#text = json.dumps(text)
    	text = json.loads(text)
    	#print(list(text.keys()))
    	path = os.path.dirname(__file__) + "\\test"


    	for key in text.keys():
        	values = text[key]
        	if values != []:
            	#print(values)
            	print(key)
            	index = 0
            	"""标签目录，内容文件"""
            	file_path = path + "\\" + key
            	if not os.path.exists(file_path):
                	os.makedirs(path + "\\" + key)
            		"""写类别标签"""
           		with open(path+"key.txt","a")as f:
                	f.write(key+"\n")
            	for value in tqdm(values):
                	try:
                    	one = r(value).strip().replace("\n","")
                    	#print(one)
                    	# print(r"F:\360下载\裁判文书网下载内容\test"+"\\"+i.replace("doc","docx"))
                	except:
                    	pass
                	with open(file_path + "\\%d.txt"%index, "a+", encoding="utf-8")as f:
                    	f.write(one)

```

之后运行cnews_group.py即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829215851320.png#pic_center"/>

cnn模型中修改类别数、标签类别<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829220006974.png#pic_center"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829220126379.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70#pic_center"/>

训练过程如下：

# 三、成果

对predict.py进行的修改，使得可以输出预测概率

```
 y_pred_cls = self.session.run(tf.nn.softmax(self.model.logits),feed_dict=feed_dict)
    max_predict = []
    for index ,item in enumerate(y_pred_cls[0]):
        #print(index)

        #print("{},{:.5%}".format(self.categories[index],item))
        max_predict.append({item:self.categories[index]})
    #return self.categories[y_pred_cls[0]]
    max_key = max([key for value in max_predict for key in value.keys()])#无法直接由值找键
    #print(max_key)
    for value in max_predict:
        for key in value.keys():
            if key == max_key:
                print("最佳预测类别为：{}，最佳预测率为{:.5%}".format(value[max_key],max_key))

```

结果为：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200829220524136.png#pic_center"/><br/>
但是在某些罪名的预测上并不太好，原因在于这些罪名下面的裁判文书缺乏，无法形成有效区分。之后进行了一次6分类即选取了罪名文本数量均在6500份以上的进行了6分类文本分类。效果较好
