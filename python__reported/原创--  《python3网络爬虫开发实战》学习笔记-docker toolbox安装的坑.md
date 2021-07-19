# 原创

： 《python3网络爬虫开发实战》学习笔记：docker toolbox安装的坑

# 《python3网络爬虫开发实战》学习笔记：docker toolbox安装的坑

docker 安装花费了我3天时间，期间一度令我绝望。<br/>
首先就是docker版本问题，进入docker官网下载的docker版本直接就是需要win10的系统，我没有发现这个系统的要求直接就下载了，结果无法运行，找了一下百度才发现原来在系统要求这里（这坑细心一点就能够发现）；接着下载了docker
toolbox，一路next到了最后，打开Docker Quickstart Terminal自动下载boot2docker，网络要么慢的不行要么报错连接不行，在csdn上找了一下发现是所谓的更新，而这个文件直接就在docker
toolbox的目录下（这个坑也不大，找一下一下子就能够找到）；但是这里也有点问题在于刚刚安装后直接断网，然后将boot2docker.iso直接复制到.docker中发现找不到或者找到了结果.docker\machine\cache中已经有了boot2docker.iso这个文件（这似乎是由于我重复安装导致的，因为卸载后.docker文件夹似乎需要手动删除）；而找不到似乎是由于安装后直接断网，导致.docker文件夹没有被创设，需要启动Docker
Quickstart Terminal后才能创建这个文件夹。反正最后找到了一个.docker文件夹将boot2docker.iso放置进入了；这其中还有一个问题就是安装直接断网后，Docker Quickstart
Terminal不出现命令框，而是需要浏览寻找bash.exe，这个问题也比较好解决，很多文章都说到了，就是bash.exe的路径复制过来就行了。不过还是推荐不要直接断网，而是联网状态下启动Docker Quickstart
Terminal，在报错后找到空.docker文件夹，将boot2docker.iso塞到.docker\machine\cache中。<br/> 美好的事情似乎要发生了，其实不然，结果在docker-machine create
--driver virtualbox default … Setting Docker configuration on the remote
daemon.这里在远程守护进程上设置docker配置时一直卡住，虽然没有出现鲸鱼图案，但是我美好的以为已经好了，结果启动Docker Quickstart
Terminal是还是卡住在这（有的记不清了（有时使用start.sh启动的），到底是 Setting Docker configuration on the remote
daemon停住还是直接什么都没有只有输入行（但是已输入就退出）），又捣鼓了很长时间发现似乎是虚拟化的问题，于是去bios中设置了虚拟化，主要是在百度上的这篇文章——《联想电脑BIOS开启虚拟化的方法》（ps:
我的是联想电脑且没有热键设置），在开机页面是按住fn+f2（就是减音量的这个件）进入Configuration的选项将其中的 Intel Virtual
Technology的选项设置成Enable的状态，保存后退出（这个坑对于电脑小白的我来说太难了，找了好久！！！！）。 然后重新启动start.sh。<br/>
虚拟化开启，一切似乎ok了，然后重新来了一遍安装卸载；但是问题又出现了——鲸鱼图案出现了，但是他并不正常，即不是下面这个样子，我的耐心耗尽了，丢了一天没有管他。重新又安装卸载来了一遍后又卡住ssl这里了，怎么解决的不太记得了，不过解决方法似乎没有用，即卡住并不是由于ssl而就是它正常的耗时。<br/>
再一次安装卸载后，又重新出现looks like something went wrong in step‘looking forvboxmanage.exe’…，这个坑在《windows7安装docker异常：looks like
something went wrong in step‘looking forvboxmanage.exe’…》文章中有提到解决方法，但是我并不是这样解决的，我直接将docker
toolbox的目录下vboxmanage.exe复制到了之前寻找bash.exe中。<br/> 最大的一个坑来了，就是To see how to connect your Docker Client to the Docker
Engine running on this virtual machine, run: docker-machine env swarm-master
…,一直卡住不动，解决方法都不靠谱，什么设置网络适配器啊等等，其中并不是这个问题（当然也可能是我不是这个问题）。参照《windows7安装docker异常：looks like something went wrong in
step‘looking
forvboxmanage.exe’…》，我最后突然得到一个灵感，就是将default重启了一下，结果成功！！！！！！！<img alt="" src="https://img-blog.csdnimg.cn/20200313085510152.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/2020031308522098.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/>
最后出现error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.28/version: open //./pipe/docker_
，参见大神fanfan4569的《error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.28/version: open //./pipe/docker_
》copySET DOCKER_TLS_VERIFY=1<br/> SET DOCKER_HOST=tcp://192.168.99.100:2376<br/> SET DOCKER_CERT_PATH=C:
\Users\Administrator.docker\machine\machines\default<br/> SET DOCKER_MACHINE_NAME=default<br/> SET
COMPOSE_CONVERT_WINDOWS_PATHS=true<br/> REM Run this command to configure your shell:<br/> REM @FOR /f “tokens=*” %i
IN (‘docker-machine env default’) DO @%i 过来搞定。
