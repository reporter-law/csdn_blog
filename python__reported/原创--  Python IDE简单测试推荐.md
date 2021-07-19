# 原创

： Python IDE简单测试推荐

# Python IDE简单测试推荐

简单入门测评<br/> 目标任务，配置好环境并运行‘Hello,World’！！

一、第一个IDE 为geany,这个IDE为我最初使用的IDE，因为我最初学习的书为《python编程-从入门到实践》，这本书推荐的这个IDE。<br/>
百度百科上的介绍<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414081456805.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
下载地址：https://geany.en.softonic.com/<br/>
开始安装：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414081316513.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
进入界面后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414084100915.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
初始安装不用配置python路径，它自己有；但是如果需要配置或者存在两个以上的python,我就建议放弃了，即使我第二次设置也觉得非常麻烦。<br/>
需要在生成选项的设置生成命令中配置<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414084704242.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

-complie 输入这个python的位置，在安全中复制对象名称，并去掉.exe，<br/> 例如对象名称为：C:
\Users\Administrator\AppData\Local\Programs\Python\Python37\python.exe

-complie的命令为：C:\Users\Administrator\AppData\Local\Programs\Python\Python37\python “%f”（注意：在python 与 “%f”之间存在空格）

同时在Execute中输入：c:\Users\Administrator\AppData\Local\Programs\Python\Python37\python “%f”（注意：在python 与
“%f”之间存在空格，且c为小写不是大写）<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414084802228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414084905821.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
这样之后输入直接运行仍不行，因为文件格式需要保存为.py格式<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414085600257.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414085537421.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
保存为.py的方式为：在名称处加上.py<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414090104119.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
如果已经是非py格式的文档，那么可以在文档（D）&gt;设置文件类型&gt;脚本语言，选中python源文件
也可以运行<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414090429704.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414090612846.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
使用感觉：<br/>
优点：相比pycharm来说，占用空间小，启动快，只是功能没有那么全，但是使用pycharm的我来说，pycahrm也不需要那么多功能，许多内置的插件都被我禁止了，因而作为第一个使用的IDE来说上手简单，适合入门。<br/>
极为重要的一点是：它是中文版的，在我初进入pycharm时发现pycharm竟然是英文版的还需要汉化时就深深的怀恋其了geany。（据说pycharm2020已经支持中文了！！）

缺点：<br/> 也是我之所以转向pycharm的一个原因，就是它使用cmd运行，会跳出来cmd命令框，个人并不是很喜欢，而看到pycharm可以在程序内运行，就换成了pycharm<br/> 参考文章<br/> 1、《01_
在windows下 Geany编辑器配置python2和python3》，链接：https://www.jianshu.com/p/d03346ae3122<br/>
2、《Geany编辑器win7环境下配置Python编程环境》，url:https://blog.csdn.net/gospellkevin/article/details/82919516

二、submit text3<br/> 作为入门的IDE，其实更加推荐submit text3,因为使用更加简单，相较于geany来说更加简单<br/> 下载地址：https://sublimetextcn.com/3/<br/>
submit text3在配置python时特别简单，至少是我迄今为止最为简单的配置python的方式<br/> 简介：

安装后<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414093011890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
个人初始感受，感觉不是特别美观。<br/>
这个的使用方法感觉和geany差不多，都是需要先保存文件然后运行，保存文件为Ctrl+S,<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414093840777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
也需要保存为.py文件格式，注意在保存类型中没有py文件格式，需要手动命令，如：test.py<br/>
保存后：<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414094011927.png"/><br/>
如果不输入名称，直接保存<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414094042125.png"/><br/>
首次运行时需要编辑解释器，个人觉得这是这个IDE的一个优点（相较于geany和pycharm来说），因为它的配置最为简单，点一下选项即可，简单就是王道！！！！！！！！！！<br/> 在工具&gt;编辑系统
中选择python即可<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414094247976.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
一个不太好的地方就是没有容易的找到运行这个键，似乎只能使用Ctrl+B这个快捷键（个人比较喜欢直接点运行选项而不是使用快捷键），而submit
text3需要在工具栏中选中立即编译或者快捷键不是很便捷<img alt="" src="https://img-blog.csdnimg.cn/20200414094829993.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
但是不调用cmd ,且能够显示运行时间也挺好的

个人使用感受：<br/> 目前最简单的IDE，体积小、启动快，几乎没有痛点。<br/> 参考：<br/>
《sublime_text3执行Python程序环境配置》，url:https://www.cnblogs.com/Chen-Zhipeng/p/9851053.html

3、现役：pycharm2019(社区版）<br/> pycharm分为社区版和专业版,社区版免费，专业版收费。

使用pycharm的大神很多，csdn上也有很多介绍<br/> 简单说说自己的使用感受<br/> 优点：<br/> 美观(
就喜欢它Theme的多样化，启动慢一点就慢一点吧），功能齐全<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200414100057198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
缺点：<br/> 启动特别慢，即使使用的各自方法，删缓存、加载插件减少、增大Xmx和xms的值也是一样

四、Wing<br/>
只有30天试用，从来白嫖的我就没有进去常识了，万一爱上了就麻烦了！<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020041411005154.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/>

五、spyder、ipython

spyder在没有按照anadonda时安装比较麻烦，需要按照各种包，比较好的一点是可以通过pip安装，但是个人不喜欢通过pip安装IDE。<br/>
此外还有ipython，个人感觉与IDLE极为相似，不喜欢这种交互式输入的方法。<br/> 据说spyder对数据科学支持较好，尚未深入，留待后续！！！

此外还有Vim、Eclipse with PyDev、Emacs、Komodo Edit、PyScripter等等

六、总结：<br/> 轻量级的推荐submit text3中文版，<br/> 功能追求的推荐pycharm.
