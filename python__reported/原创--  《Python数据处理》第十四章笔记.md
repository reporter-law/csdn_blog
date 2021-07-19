# 原创

： 《Python数据处理》第十四章笔记

# 《Python数据处理》第十四章笔记

### 《Python数据处理》第十四章笔记

# 一、Python日志

源码及其注释

```
import logging

```

from datetime import datetime

def start_logger():<br/> ‘’‘日志初始化设置、文件名（时间）、DEBUG为调试级别(级别导致输出内容的不同）、日志的记录格式、日期格式’’’

```
logging.basicConfig(filename='daily_report_error_%s.log' %
                    datetime.strftime(datetime.now(), '%m%d%Y_%H%M%S'),
                    level=logging.ERROR,
                    format='%(asctime)s %(message)s',
                    datefmt='%m-%d %H:%M:%S')


def main():
	start_logger()
	'''日志记录,SCRIPT:为日志输出前缀，logging。debug代表输出级别'''
	logging.debug("SCRIPT: I'm starting to do things!")

	try:
   	 	'''此为执行的主内容'''
    	20 / 0
	except Exception:
    	logging.exception('SCRIPT: We had a problem!')
    	logging.error('SCRIPT: Issue with division in the main() function')

 logging.debug('SCRIPT: About to wrap things up!')

if __name__ == '__main__':
 main()

```

此处有不同：

```
源码：
 
logging.basicConfig(filename='/var/log/my_script/daily_report_%s.log' %
                    datetime.strftime(datetime.now(), '%m%d%Y_%H%M%S'),
                    level=logging.DEBUG,
                    format='%(asctime)s %(message)s',
                    datefmt='%m-%d %H:%M:%S')
  #/var/log/my_script/为路径
logging.basicConfig(filename='daily_report_error_%s.log' %
                    datetime.strftime(datetime.now(), '%m%d%Y_%H%M%S'),
                    level=logging.ERROR,
                    format='%(asctime)s %(message)s',
                    datefmt='%m-%d %H:%M:%S')

```

理解：其实就是print方法的模块化

# 二、邮件

## 一、问题：

email不用下载，下载还出错。

但是函数名字盖了，需要变为<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519173929493.png"/><br/> 参见《Python3.5
email发送邮件，包含txt、图片、HTML、附件》，链接: [link](https://blog.csdn.net/wjoxoxoxxx/article/details/77944126?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158988083919725222413538%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&amp;request_id=158988083919725222413538&amp;biz_id=0&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-2-77944126.first_rank_ecpm_v2_pc_rank_v3&amp;utm_term=python+email)
.

而ConfigParser 需要下载<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519174039508.png"/><br/> import
ConfigParser 会报错<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051917440519.png"/>

需要

```
import configparser

```

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519174651546.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020051917470554.png"/>

太复杂，最后放弃了

成功的程序参见《《python调试》python发邮件出现smtplib.SMTPServerDisconnected: Connection unexpectedly
closed问题的解决办法》，链接: [link](https://blog.csdn.net/jiangsujiangjiang/article/details/80324098?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&amp;depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
.

注：不需要用密码而是授权码，<br/> QQ授权码的获取：<br/> 第一步：<br/>
登录QQ邮箱<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181310969.png"/><br/> 第二步：<br/>
选着账户选项，<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181354112.png"/>

第三步：<br/> 下拉找到POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务，点击开启POP3/SMTP服务 (如何使用 Foxmail
等软件收发邮件？)<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181506346.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181607203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
即可获取授权码<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181714781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

之后即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181735380.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200519181800374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
