# 原创

： 利用pycharm简单实现多进程

# 利用pycharm简单实现多进程

python多进程需要使用进程池

```
 from multiprocessing.pool import Pool
 import time
 def worker(x):
	print("worker"+"{number}".format(number=x))
	time.sleep(1)
	return
	starttime = time.time()
	GROUP_START = 1
	GROUP_END = 20
	if __name__ == '__main__':
		pool = Pool(4)
		group = ([x for x in range(GROUP_START, GROUP_END + 1)])#process中的group基本不用，但这个不是process，但是这个不是
		pool.map(worker,group)
		pool.close()
		pool.join()
	endtime = time.time()
	dtime = endtime - starttime
	print("程序运行时间：%.8s s" % dtime)

```

但是利用pycharm的允许并行允许可以简单实现多进程

运行----编辑配置-----允许并行允许<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200424163538115.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200424163607577.png"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200424163629278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70"/><br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200424163707351.png"/>
