# 原创

： selenium的namespace错误与无法定位：NamespaceError: An attempt was made to create...andUnable to locate elemen ：

原力计划

# selenium的namespace错误与无法定位：NamespaceError: An attempt was made to create...andUnable to locate elemen

### selenium报错:NamespaceError: An attempt was made to create or change an object in a way which is incorrect with regard to namespaces'

说明：selenium中的窗口似乎视角窗口柄、窗口句柄，我在此处就叫窗口了

# 一、报错

第一个报错：namespace error<br/> ‘selenium.common.exceptions.InvalidSelectorException: Message: Given xpath expression’
“/html/body/div/div[4]/div[2]/diy:lawyee[2]/div[3]/div[6]/div/a[2]” is invalid: '‘NamespaceError: An attempt was made to
create or change an object in a way which is incorrect with regard to namespaces’

第二个报错： Unable to locate element<br/> 但是出现另一个问题：就是无法定位，出现报错：

```
selenium.common.exceptions.NoSuchElementException: Message:: //div[@class="listTMain clearfix"]

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528133015570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是确实是在元素所在的窗口，使用

```
browser.switch_to.window(browser.window_handles[1])

```

# 二、原因

xpath中有：<br/> xpath语法

```
'//diy:lawyee[2]/div[@class="LM_tool clearfix"]/div[@class="fr tool_All"]/a[1]/label'

```

由于语法中存在标签：diy:lawyee导致的namespace错误

去掉 这个标签diy:lawyee，不报namespace error

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528123435271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第二个问题的原因：<br/>
浏览器的原因，我使用的是firefox浏览器，浏览器窗口定位的问题；例如：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528133513584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

此时窗口处于文书列表页

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200528133542201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
此时窗口处于首页

# 三、解决方法

第一个报错的解决方法，就是去掉标签，重新写一个不含这个会导致namespaceerror的标签

第二个报错解决方法：<br/> 但是重写后又会出现第二个报错：不能定位元素

这个报错也花了很久时间才发现，原因不明

在chrome浏览器中需要进行窗口移动，要在那个窗口进行操作就要移动到哪一个窗口，（默认处于第一个窗口）例如需要在第一个窗口操作则移至第一个窗口，命令为：

```
browser.switch_to.window(browser.window_handles[1])

```

其中的数字为试图移动到的窗口，0为第一个窗口，而1为第二个窗口，依次类推

但是在firefix中会自动移至当前窗口（默认是当前操作窗口），本以为不用这一命令，但是元素定位时却定位不到；然而使用该命令却出现以下报错：

```
IndexError: list index out of range

```

解决方法为：我想到的解决方法就是向chrome一样进行窗口移动，先由当前窗口移至第一个窗口，然后移动回来。<br/> 命令类似为：

```
browser.switch_to.window(browser.window_handles[0])
browser.switch_to.window(browser.window_handles[1])

```

第二个是要操作的窗口，我要操作的窗口为第二个窗口，<br/> 各位需要操作的窗口是什么就按照窗口所在的位置进行变动即可，如第三个则为：

```
browser.switch_to.window(browser.window_handles[3])

```

这样就可以了
