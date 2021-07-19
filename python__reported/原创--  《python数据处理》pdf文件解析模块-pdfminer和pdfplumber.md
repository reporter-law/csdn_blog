# 原创

： 《python数据处理》pdf文件解析模块：pdfminer和pdfplumber

# 《python数据处理》pdf文件解析模块：pdfminer和pdfplumber

pdfplumber以pdfminer为基础，但是pdfminer的操作过于复杂且代码过于冗长。<br/> 注：pdfminer在python3.0以上为pdfminer3k<br/> pdfminer3k 实现解析的代码：

```
from pdfminer.pdfparser import PDFParser
from pdfminer.pdfdocument import PDFDocument
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.pdfpage import PDFTextExtractionNotAllowed,PDFPage
from pdfminer.layout import LTTextBoxHorizontal, LAParams
from pdfminer.converter import PDFPageAggregator
import os

paths = os.listdir('F:\新建文件夹\捕诉')
for path_ in paths:
print(path_)
path = 'F:\新建文件夹\捕诉'+'\\' +path_#为什么两条斜杠，是因为转义吗？
open_pdf = open(path,'rb')
pdf_file = PDFParser(open_pdf)
#1、PermissionError: [Errno 13] Permission denied: 'F:\\新建文件夹'——
# 2、误产生的原因是文件无法打开，可能产生的原因是文件找不到，或者被占用，或者无权限访问，或者打开的不是文件，而是一个目录。
doc = PDFDocument(pdf_file)
#print(type(doc))&lt;class 'pdfminer.pdfparser.PDFDocument'
#print(type(pdf_file))&lt;class 'pdfminer.pdfparser.PDFParser'&gt;
'''可能是需要将文件转入包分析内格式'''
# 检测文档是否提供txt转换，不提供就忽略

    # 创建pdf资源管理器 来管理共享资源（字体的导入）
srcmgr = PDFResourceManager()
    # 创建一个pdf设备对象
device = PDFPageAggregator(srcmgr, laparams=LAParams())#聚合器
    # 创建一个pdf解释器对象
interpreter = PDFPageInterpreter(srcmgr, device)
#print(doc.get_outlines())

#print(PDFPage.get_pages(doc))# 获取page列表
    # 循环遍历列表，每次处理一个page的内容
for page in PDFPage.create_pages(doc):
    #print(page)
    interpreter.process_page(page)
    #之前就是为了为这个解析提供工具
#print(type(page))

# 接受该页面的LTPage对象 #这里layout是一个LTPage对象 里面存放着 这个page解析出的各种对象
    layout = device.get_result()#页面中的结果
#print(layout)
    #print(x)
    for x in layout:
        if hasattr(x, 'get_text'):#进行if判断是为了剔除非文字
            with open('pdfduqu.txt', 'a+', encoding='utf-8') as f:
                results = x.get_text()
                f.write(results + '\n')
            '''只有最后一页'''

        # 最后关闭原始pdf文件
open_pdf.close()
'''太复杂了'''
#layout 在interpreter下面就有三页，可能是由于不在下面，面对的是最后一页的解析
#WARNING:root:GBK-EUC-H  缺失中文解码字体

```

pdfplumber 实现代码：

```
import pdfplumber
path = 'E:\桌面文件\捕诉模式\常态社会与运动式治理_中国社会治安治理中的_严打_政策研究_唐皇凤.pdf'
pdf = pdfplumber.open(path)

for page in pdf.pages:
'''pages为函数？'''
print(page.extract_text())

with open('简单的pdf.txt', 'a+', encoding='utf-8')as f:
    '''需要进行编码'''
    f.write(page.extract_text())

```

然而pdfplumber作者最近一直在更新，结果出来问题

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501173851953.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
最新版本的出现问题<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501173933134.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
第一个报错是由于之前将pdfminer删除了，下载下来就可以了

第二个报错就是更新导致的<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020050117402580.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
将导入错误的注释掉即可

或者换回0.5.16即可

现在成功解决：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200501174834219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>
