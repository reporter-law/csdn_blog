# 原创

： Pandas合并excel文件错位现象的解决 ：

原力计划

# Pandas合并excel文件错位现象的解决

### Pandas合并excel文件错位现象的解决

# 一、文件错位现象

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200527110934333.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200527110958683.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

说明：原本想将多列变为一列，以便后续的可视化处理，但是合并后出现这样的错位

原本试图通过pandas的cancat()方法中的参数解决，但是没有效果。

pandas的cancat()
方法参数解释,参见《pandas数据合并与重塑（pd.concat篇）》，链接: [link](https://blog.csdn.net/mr_hhh/article/details/79488445?ops_request_misc=&amp;request_id=&amp;biz_id=102&amp;utm_term=pandas%20cancat&amp;utm_medium=distribute.pc_search_result.none-task-blog-2~blog~sobaiduweb~default-0-79488445)
.

# 二、原因

既然参数中找不到解决问题的原因，我就又重新复习了一遍cancat()方法。<br/> 原本以为是excel文件索引的问题，即假设：第一个文件的列为1-10，则合并的第二个文件的列索引应为11-20,如此循环。

但是在其他的excel文件合并时，列索引可以相同，合并后依旧是沿着原列索引后面增加，完全不需要人工设置列索引之间的对齐。

重新看了一下表头，发现合并后的excel是以原excel文件的表头作为新的汇总表的表头的，接下来的排列也是如此，出现错位，实质上是依据表头的不同而不同的，<br/>
因为问题的核心在文件的格式不同，即不是同一个数据集，或者说格式没有整齐划一，表头没有一致，这个是我的锅，原本写入excel中就是希望表头后补可能更好合并

修改后，先写入excel文件的表头，保证每个excel文件的表头一致，然后进行合并

# 三、解决

原来试图简化的代码为：

```
#ws.cell(row=1, column=1, value='分词')
#ws.cell(row=1, column=2, value='频率')
#ws.cell(row=1, column=3, value='文书名')

ws.cell(row=i + 1, column=1, value=datas[1][i][0])
ws.cell(row=i + 1, column=2, value=datas[1][i][1])
ws.cell(row=i + 1, column=3, value=datas[0])

```

将表头的内容添加进去即可

```
ws.cell(row=1, column=1, value='分词')
ws.cell(row=1, column=2, value='频率')
ws.cell(row=1, column=3, value='文书名')

ws.cell(row=i + 1, column=1, value=datas[1][i][0])
ws.cell(row=i + 1, column=2, value=datas[1][i][1])
ws.cell(row=i + 1, column=3, value=datas[0])

```

生成的excel文件内容（没有添加表头前）：

添加表头后：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200527112739423.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

合并：

```
def xlsx_concat(self):
    """xlsx文档合并"""

    input_files = 'J:\PyCharm项目\项目\项目二_文书内容提取\输出模块\可视化输出\\xslx写入'
    print('读取到了第一个文件.............................................')
    output_file = 'J:\PyCharm项目\项目\项目二_文书内容提取\输出模块\可视化输出\\xslx写入\\test汇总表.xlsx'
    #需要创建，否则没有输出对象
    print('读取到了第二个文件.............................................')
    all_workbook = glob.glob(os.path.join(input_files, '*.xlsx'))
    #print(all_workbook)

    data_frames = []
    '''重点来了，遍历工作簿、工作表，簿为列表，表为字典'''
    for workbook in all_workbook:
        all_sheets = pd.read_excel(workbook, sheet_name=None, index_col=None)
        for worksheet_name, data in all_sheets.items():
            data_frames.append(data)#sheets内容为表名与表内容
    all_data = pd.concat(data_frames)#axis即竖连接还是横连接
    print(data_frames)
    writer = pd.ExcelWriter(output_file)
    all_data.to_excel(writer, sheet_name='all_output', index=False)
    writer.save()

```
