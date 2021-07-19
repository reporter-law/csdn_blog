# 原创

： selenium节点（元素）遍历的疑惑

# selenium节点（元素）遍历的疑惑

### selenium节点的遍历

# 一、节点遍历是什么

例如：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200609113919935.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
由于裁判文书网只显示前600个，我的思路就是通过关键词的限定实现内容在600条以内，因而完整的下载需要进行关键词的遍历<br/>
html：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200609114211910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、问题

直接进行遍历会报错，原因不明<br/> 如：

```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait

browser = webdriver.Firefox()

"""网页获取"""
browser.get('http://wenshu.court.gov.cn/website/wenshu/181217BMTKHNT2W0/index.html?pageId=0a8bea45ec529d8391dd57f1a421ae4e&amp;s21=%E8%AE%A4%E7%BD%AA%E8%AE%A4%E7%BD%9A')
wait = WebDriverWait(browser,20)
"""进行内部遍历获取，通过关键字进行限定"""
for number in range(1,35):
	keywords = wait.until(EC.presence_of_element_located((By.XPATH, '//*[@id="j3_%d_anchor"]'%number)))
	print(keywords)
	keywords.click()
	time.sleep(1)
	button = wait.until(EC.presence_of_element_located((By.XPATH, '//div[@class="LT_Filter_right clearfix"]/p[2]/i['
                                                              '@class="fa fa-close"]')))

	keywords.click()

```

每次都是第一个元素可以点击，但是接下来遍历的第二个元素都会报错，timeout，即超时<br/> 不是%d不能传入，因为第一个可以传入

# 三、解决方法

问题产生原因不明，解决原因也不明<br/> 思路，既然每次第二个元素超时，那就关闭浏览器，使得每次只点击的第一个元素；即点击一个元素关闭一次浏览器，然后重启浏览器。这样就需要每次启动浏览器传入需要遍历的值

```
def selenium(number):
"""尝试遍历"""
print()
browser = webdriver.Firefox()

"""网页获取"""
browser.get('http://wenshu.court.gov.cn/website/wenshu/181217BMTKHNT2W0/index.html?pageId=0a8bea45ec529d8391dd57f1a421ae4e&amp;s21=%E8%AE%A4%E7%BD%AA%E8%AE%A4%E7%BD%9A')
wait = WebDriverWait(browser,20)
"""进行内部遍历获取，通过关键字进行限定"""

keywords = wait.until(EC.presence_of_element_located((By.XPATH, '//*[@id="j3_%d_anchor"]'%number)))
print(keywords)
keywords.click()
time.sleep(1)
browser.close()
for number in range(1,10):
	selenium(number)	

```

# 四、结语

问题虽然解决了，但是原理不明，并不是xpath语法不对，问题在于为什么浏览器只能点击第一个元素，清除后再次点击就会超时？？？？？？
