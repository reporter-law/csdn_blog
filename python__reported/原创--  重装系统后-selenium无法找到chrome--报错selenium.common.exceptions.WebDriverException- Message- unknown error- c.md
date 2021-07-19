# 原创

： 重装系统后：selenium无法找到chrome--报错selenium.common.exceptions.WebDriverException: Message: unknown error: c

# 重装系统后：selenium无法找到chrome--报错selenium.common.exceptions.WebDriverException: Message: unknown error: c

### 重装系统后：selenium无法找到chrome--selenium.common.exceptions.WebDriverException: Message: unknown error: cannot find Chrome binary

# 一、报错

```
selenium.common.exceptions.WebDriverException: Message: unknown error: cannot find Chrome binary

```

翻译过来为：selenium.common.exceptions.WebDriverException：消息：未知错误：找不到Chrome二进制文件

即找不到chrome浏览器

# 二、解决方法

添加chrome路径：

```
ops.binary_location = r'I:\Program Files (x86)\Google\Chrome\Application\chrome.exe'

```

ops是传递给option的对象<br/> 完整为：

```
from selenium.webdriver.chrome.options import Options
ops.binary_location = r'I:\Program Files (x86)\Google\Chrome\Application\chrome.exe'（此处是我的chrome位置，需要在r""中填上自己的chrome位置）
browser = webdriver.Chrome(options=ops)

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521205125522.png"/><br/> 这个是我自己设置的输出，出现代表着正确

# 三、第二个报错：

```
selenium.common.exceptions.WebDriverException: Message: Can not connect to the Service chrome

```

连接错误，需要

ping localhost

如果为ping的结果为：<br/> 一般错误<br/> 一般错误<br/> 一般错误<br/> 这样的结果<br/> 则存在错误

# 四、解决方法：

关闭防火墙<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521205238687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521205257929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
再次，

```
ping localhost

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200521205359476.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
参见《mac selenium.common.exceptions.WebDriverException: Message: Can not connect to the Service
chromedri》链接: [link](https://blog.csdn.net/qq_40270754/article/details/101022414).
