# 原创

： selenium的两种sendkeys差异 ：

原力计划

# selenium的两种sendkeys差异

### selenium的两种sendkeys差异

预览：<br/> 报错：

```
'FirefoxWebElement' object has no attribute 'sendkeys'

```

方法：

```
actions.move_to_element(time_send).send_keys("2019-01-01").perform()#开始日期

```

成功截图：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200629132954515.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 一、两种需要输入的文本框

此处均以裁判文书网为例

## （一）第一种：常态的文本输入框

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200629130331129.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
元素类型一般均有input,即最后一个元素标签是“input"<br/> 例如：以下为该元素文本框的xpath路径，常态的这种文本框，等等输入内容的元素标签均为…框起来的<br/> l<br/>
//*[@id="_view_1540966814000"]/div/div[1]/div[2]/input

## （二）第二种：特殊的文本输入框

此处裁判日期处的文本框就是特殊的文本框，可以进行选择，但是一个个选择命令无疑比较麻烦，比较好的的方法就是sendkeys

其元素元素标签就可能不是“input"，，此处为input

```
&lt;input class="laydate-icon ldt dropdown-text" id="cprqStart" type="text" style="width:117px;" lay-key="1"&gt;

```

虽然都是…框起来的，但是后者点击时会加载一个可选的js文件即<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200629131357330.png"/>

# 二、问题

第二种文本框使用sendkeys时就会报错

```
"""审判日期：2019"""
        time_send = wait.until(EC.element_to_be_clickable((By.XPATH, '//*[@id="cprqStart"]')))
        time_send.click()
        time_send.sendkeys("2019-01-01")

```

此时报错

```
'FirefoxWebElement' object has no attribute 'sendkeys'

```

# 三、解决方法

参见罗 小双 和 熊 虎：《Selenium WebDriver
中鼠标和键盘事件分析及扩展》，链接: [《Selenium WebDriver 中鼠标和键盘事件分析及扩展》](https://www.ibm.com/developerworks/cn/java/j-lo-keyboard/).

在这篇文章中发现selenium中的sendkeys竟然存在两类，一类是常用的WebElement.sendKeys，一类是Selenium
WebDriver的Actions类中的sendKeys方法，介绍参见大鵬：《【学习笔记】Selenium
WebDriver的Actions类中的sendKeys方法和WebElement.sendKeys方法的区别》，链接: [【学习笔记】Selenium WebDriver的Actions类中的sendKeys方法和WebElement.sendKeys方法的区别》](https://blog.csdn.net/lchydp1979/article/details/78374280?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&amp;depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
.

既然WebElement.sendKeys不行，报错”FirefoxWebElement’ object has no attribute ‘sendkeys’“,那就换一种

```
"""审判日期：2019"""
        time_send = wait.until(EC.element_to_be_clickable((By.XPATH, '//*[@id="cprqStart"]')))
        time_send.click()
        actions.send_keys_to_element(time_send,"2019-01-01")

```

actions.send_keys_to_element，这个是actions自动提示的方法，不知道为什么不行，可能自己用错了<br/> 于是换成了

```
 """审判日期：2019"""
        time_send = wait.until(EC.element_to_be_clickable((By.XPATH, '//*[@id="cprqStart"]')))
        time_send.click()
        actions.move_to_element(time_send).send_keys("2019-01-01").perform()#开始日期

```

成功完成sendkeys任务
