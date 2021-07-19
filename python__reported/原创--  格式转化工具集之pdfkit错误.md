# 原创

： 格式转化工具集之pdfkit错误

# 格式转化工具集之pdfkit错误

### 格式转化工具集之pdfkit错误： raise IOError("wkhtmltopdf exited with non-zero code {0}. error:\n{1}"

# 一、报错

代码：

```
OSError: wkhtmltopdf exited with non-zero code 1. error:

```

这是一个不明原因的报错

二、解决方法

最终发现这源于转换的pdf文件名中不能有特殊字符

转换代码：

```
inport pdfkit
pdfkit.from_url(url, file)

```

是指这个file不能有特殊字符<br/> 如file为：

```
讲座报道 | 王燕玲:《认罪认罚从宽制度下智能精准量刑的理论与实践》.pdf

```

时就会报错<br/> 使得输出的pdf文件名没有特殊字符，通过正则提取中文即可

```
title = "".join(re.findall(r'[\u4e00-\u9fa5]+',artical["article"]["title"]))

```

这个title就是文件名

完整代码：这是我对搜狗微信文章所作的url转pdf保存，前期已经获取url并保存到txt中了

```
import os,glob
import pprint
import re

import pdfkit
import json
from tqdm import tqdm

def url_to_pdf():
 for i in tqdm(glob.glob(os.path.join(r"J:\PyCharm项目\package_test_\搜狗文章爬虫\artical", "*"))):
    with open(i, "r")as f:
        artical = json.load(f)
        # print(artical)
        url = artical["article"]["url"]

        title = "".join(re.findall(r'[\u4e00-\u9fa5]+',artical["article"]["title"]))
        print(title,type(title))
        print(url)
        if url:
            path = os.path.dirname(__file__) + "\\pdf文章"
            if not os.path.exists(path):
                os.makedirs(path)
            file =  path+r"\\{}.pdf".format(title)
            print(file)
            pdfkit.from_url(url, file)
url_to_pdf()

```

# 三、解决过程

## （一）url

我首先怀疑是url格式的问题<br/>
因为url是这样的，中间有个*<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200822144713723.png#pic_center"/><br/>
这是一个完整的url,但是*后面的不能和前面一样成蓝色，是否是格式出了问题

于是通过requests测试，结果没有问题

## （二）pdfkit版本

于是我就怀疑是不是pdfkit版本的问题，因为pdfkit已经是2017年的了，长期没有更新，但是wkhtmltopdf 一直在更新，于是怀疑是不是版本不匹配，结果换了版本也是一样。

## （三）契机

在作wkhtmltopdf 测试时将file 命名为1.pdf结果同样的url竟然可以转换，于是是文件名的可能性就大了，接着便通过replace对文件名进行清洗，发现是其中的"|"
符号导致的，继续进行后续的pdf转换，继续报错，按照上述步骤继续替换发现特殊"导致的<br/>
于是最终得出结论，这是特殊符号导致的问题，通过正则表达式进行中文匹配后输出文件名就成功了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200822145435215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70#pic_center"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200822145451967.png#pic_center"/>
