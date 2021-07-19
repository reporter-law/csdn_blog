# 原创

： 重装系统后：tesseract 和 图片灰度化报错-PIL.UnidentifiedImageError: cannot identify image file

# 重装系统后：tesseract 和 图片灰度化报错-PIL.UnidentifiedImageError: cannot identify image file

### 图片灰度化报错：PIL.UnidentifiedImageError: cannot identify image file

# 一、现象

## （一）第一个报错

```
import pytesseract#tesserocr 变成了pytesseract
from PIL import Image
images = Image.open('验证.png')
images = images.convert('L')
print(pytesseract.image_to_string(images))
#image_to_text(images)#已经没有了
'''验证失败'''
#灰度化

images.show()
#print(pytesseract.image_to_string(image))
#二值化
threshold = 40
table =[]
for i in range(256):
	if i &lt; threshold:
    	table.append(0)
	else:
    	table.append(1)
image = images.point(table,'1')
result = pytesseract.image_to_string(image)
print('ok')
print(result)

```

验证时出现路径错误：<br/> 原报错就是此处，进入这个界面需要最后一个报错路径处打开

进入此处<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523195802359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
报错地点在这里：报错时位置并不是这样（此处已经更改完成了）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523195709724.png"/>

## （二）第二个报错

报错

```
PIL.UnidentifiedImageError: cannot identify image file 'J:\\PyCharm项目\\项目\\项目二_文书内容提取\\提取模板模块\\parrot_new.png'

```

# 二、解决过程

## 第一个报错解决

更新路径即找到路径<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523200202216.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
将路径更新为现在路径即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523200325565.png"/>

## 第二个报错解决过程

更新pillow

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523193846529.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
更换另一个图片后可以说明可能是该图片或者是其路径有问题<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523194237614.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
更换路径后仍然一样：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523194519991.png"/>

重新对图片进行检查发现，图片错误<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523194452680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

只能对图片进行更新！！！！！！！

重新下载后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020052319500041.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

```
from PIL import Image

image_path ='J:\PyCharm项目\项目\项目二_文书内容提取\输出模块\parrot_new.png'
image = Image.open(image_path)
im_gray = image.convert('L')
im_gray.show()

```

成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200523195207623.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
