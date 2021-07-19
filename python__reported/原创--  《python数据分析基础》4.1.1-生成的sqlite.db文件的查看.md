# 原创

： 《python数据分析基础》4.1.1：生成的sqlite.db文件的查看

# 《python数据分析基础》4.1.1：生成的sqlite.db文件的查看

在《《python数据分析基础》4.1.1：报错——sqlite3.OperationalError: table csv has 5 columns but 4 values were
supplied》生成了csv_database.db这个文件，但是直接记事本打开为乱码<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428175806169.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
pycharm打开为乱码：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428175838541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
使用sqlite的可视化工具，sqlitespy<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428175957179.png"/><br/>
和mms-v2.1.1-community-windows都没有打开<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428180112987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
直到使用SQLiteExpertPersSetup64
才打开了<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428180337836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

设置比较简单，直接File&gt;Opendatabase
即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428180440107.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
在这个页面选中data即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200428180502860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
成功图为：
