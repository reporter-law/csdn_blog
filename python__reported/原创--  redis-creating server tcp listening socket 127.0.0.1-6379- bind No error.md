# 原创

： redis:creating server tcp listening socket 127.0.0.1:6379: bind No error

# redis:creating server tcp listening socket 127.0.0.1:6379: bind No error

### redis:creating server tcp listening socket 127.0.0.1:6379: bind No error

# 一、解决方法

解决链接：链接: [‘redis-server’ 不是内部或外部命令，也不是可运行的程序或批处理文件](https://www.cnblogs.com/shanjinghao/p/12892638.html).

按照步骤来一遍

```
redis-cli
shutdown
exit
redis-server.exe  J:\python_software\redis\redis.windows.conf  ps这个redis.windows.conf  需要找到你自己的路径

```

# 二、成功
