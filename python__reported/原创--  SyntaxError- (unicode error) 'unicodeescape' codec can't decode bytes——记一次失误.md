# 原创

： SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes——记一次失误

# SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes——记一次失误

读取文件时报错：<br/> SyntaxError: (unicode error) ‘unicodeescape’ codec can’t decode bytes in position 105-106: truncated
\uXXXX escape<br/> 文件路径为：F:…(省略了中间路径）\urls.txt<br/> 在file_path = 'F:…（省略了中间路径）urls.txt’中没有出现报错，以为这种写法可以。<br/>
当出现报错时，去pycharm中修改文件编码结果没有用。<br/> 找到博主Your-Nikee《SyntaxError: (unicode error) ‘unicodeescape’ codec can’t decode bytes
in position 2-3: truncated \UX》才知道还是路径问题，路径必须加上双斜杠<br/> ‘F:\…\urls.txt’

读取成功<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200405152130477.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

[1]https://blog.csdn.net/YourNikee/article/details/102738764
