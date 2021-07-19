# 原创

： python获取2020年国家统计局省市县三级数据

# python获取2020年国家统计局省市县三级数据

### python获取2020年国家统计局省市县三级数据

# 一、数据来源

国家统计局2020年最新的数据<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20201228111800900.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20201228111840250.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

# 二、获取思路

寻找url的规律<br/> 所有省份页面：

```
http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/index.html

```

城市页面：

```
http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/11.html

```

失去页面：

```
http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/11/1101.html

```

总结url具有鲜明的层次性，年份2020，城市11，区01<br/> 因而迭代获取相关url标签

省级：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20201228112332288.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

市级<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20201228112404903.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
区级

# 三、完整代码

```
下面展示一些 `内联代码片`。
import sys,os,re,requests
from lxml import etree
from crawler_tools.user_agent import user_agent as u
class Citys():
	def __init__(self):
    	self.url = "http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/"
    	self.file = os.path.dirname(__file__)
	def get_url(self):
    	header = {
        	'Cookie': 'SF_cookie_1=72991020',
        	'User-Agent': u.user_agent()["User-Agent"]}
    	r1 = requests.get(self.url,headers=header)
    	r1.encoding = r1.apparent_encoding
    	return r1.text
	def xpath_parse(self):
    	#省
    	lxml = etree.HTML(self.get_url())
    	provinces = lxml.xpath("//tr/td/a/text()")
    	#市
    	citys = lxml.xpath("//tr/td/a/@href")
    	for n,i in enumerate(citys):
        	url = 'http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/'+i
        	print("市：",url)
        	r2 = requests.get(url,headers=u.user_agent())
        	r2.encoding = r2.apparent_encoding
        	countys = etree.HTML(r2.text).xpath("//tr/td[2]/a//text()")
        	#print(xpath)
        	#县
        	countys_href = etree.HTML(r2.text).xpath("//tr/td[2]/a/@href")
        	#print(countys)
        	for ns,county in enumerate(countys_href):
            	url = 'http://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/2020/'+county
            	print("县:",url)
            	r3 = requests.get(url, headers=u.user_agent())
            	r3.encoding = r3.apparent_encoding
           		zones = etree.HTML(r3.text).xpath("//tr/td[2]/a//text()")
            	for zone in zones:
                	yield provinces[n]+","+countys[ns]+","+zone

	def download(self):
    	for i in self.xpath_parse():
        	with open(self.file+"\provinces_city_zone.txt","a+",encoding="utf-8")as f:
            	f.write(i+"\n")
Citys().download()

```

# 四、成果

# 四、获取地址

直接获取省市县三层次数据: [Github](https://github.com/reporter-law/province_and_citys).
