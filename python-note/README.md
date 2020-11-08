# atexit.register

```python
import atexit
@atexit.register
def func():
#    程序退出时调用此函数
```



# 装饰器和闭包

```python
# 闭包
def decorate_func(func):
	a = 1   # 不可变
	b = []
	def inner():
		nonlocal a # 不可变 ，引用外面函数的变量，需要nonlocal
		a += 1     
		b.append(3)  # 可变， 直接引用
		# a, b 由于用了外面函数的量，就被绑定到了内部函数上，成为了自由变量 ，这里就构成了一个闭包
		return func
	return inner
    

# 计时装饰器
def clock(func):
	def inner(*args,**kwargs):
		start = time.time()
		res = func(*args,**kwargs)
		args_str = [repr(arg) for arg in args]
		args_str = ', '.join(args_str)
		kwargs_str = [k+"="+repr(v) for k,v in sorted(kwargs.items())]
		kwargs_str = ', '.join(kwargs_str)
		print("func name:{} ({}, {}),time: {}s".format(func.__name__, args_str, kwargs_str,time.time() - start))
		return res
	return inner

# 等价于 add = clock(add)
@clock
def add(a,b):
    return a+b
```

# 异常处理

```python
使用try 会在捕获异常后继续执行
不适用try 用 raise 直接抛出异常程序会中断执行，退出
try:
    # 要捕获异常的代码
except Exception as e:
    # 捕获到了异常
    print(e)
else:
    # 正常运行
finally:
    # 都运行
    
raise ValueError("111")  # 主动抛出异常
```



# 多线程/多进程

- 多线程

```python
import os
import time
import threading
def tstart(arg):
    var = 0
    for i in range(100000000):
        var += 1

if __name__ == '__main__':
    t1 = threading.Thread(target=tstart, args=('This is thread 1',))
    t2 = threading.Thread(target=tstart, args=('This is thread 2',))
    start_time = time.time()
    t1.start()
    t2.start()
    t1.join()
    t2.join()
    print("Two thread cost time: %s" % (time.time() - start_time))
    start_time = time.time()
    tstart("This is thread 0")
    print("Main thread cost time: %s" % (time.time() - start_time))
```

- 多进程

```python
from multiprocessing import Process  
import os, time

def pstart(arg):
    var = 0
    for i in range(100000000):
        var += 1

if __name__ == '__main__':
    p1 = Process(target = pstart, args = ("1", ))
    p2 = Process(target = pstart, args = ("2", ))
    start_time = time.time()
    p1.start()
    p2.start()
    p1.join()
    p2.join()
    print("Two process cost time: %s" % (time.time() - start_time))
    start_time = time.time()
    pstart("0")
    print("Current process cost time: %s" % (time.time() - start_time))
```

- 线程池，进程池

```python
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor
import time,os

def tstart(arg):
    var = 0
    for i in range(100000000):
        var += 1
    return var
def finished(future):
	print(id(future))
	print("thread has finished")

if __name__ == '__main__':
	executor=ThreadPoolExecutor(max_workers=3)
	# 最大进程/线程数 为3
    start = time.time()
	f1 = executor.submit(tstart,"1")
	f2 = executor.submit(tstart,"2")
	# 提交任务
    f1.add_done_callback(finished)
	f2.add_done_callback(finished)
    # 回调函数，即完成时会执行的函数
	executor.shutdown(True)
    # 等待全部完成
	print(time.time()-start)
	start = time.time()
	tstart("1")
	print(time.time()-start)
```



# math

```python
# 返回点（dx，dy）对于（0，0）的弧度值 -pi~pi
atan2(dy,dx)  
```

# 字符串

```python 
s.count('a')  # 子串个数（不重叠）
s.split(' ')  # 返回以空格隔开的子串列表
```

# 具名元组 | namedtuple

```python
from collections import namedtuple
city = namedtuple('city','x y z') # 'x y z'可以是可迭代的字符串对象 如 ['x','y','z'] 
city_inst = city(1,2,3)
city_inst.x   # 等价于city_inst[0]
city_inst.y
city_inst.z
```

# 排序 

```python
x = [2,3,1,4]
x1 = sorted(x)  # 返回新对象
x.sort()   # 直接在原先的基础上排序

from operator import itemgetter, attrgetter
y = [(2,4),(2,3),(1,5),(3,4)]
y.sort(key=lambda x:x[0])
y.sort(key=itemgetter(0))
y.sort(key=itemgetter(0,1))
attrgetter('age') 

def cmp(x,y):
    if x[0] == y[0]:
        return x[1]>y[1]
    return x[0]<y[0]

from collections import namedtuple
t = namedtuple('t','x y')
t.__lt__ = cmp
x = [t(2,3),t(2,4),t(1,5),t(3,4)]
x.sort()
```

# logging

```python
# 同时输出到文件和控制台
log_format = '%(asctime)s %(message)s'
logging.basicConfig(stream=sys.stdout, level=logging.INFO,
    format=log_format, datefmt='%m/%d %I:%M:%S %p')
fh = logging.FileHandler('log.txt')
fh.setFormatter(logging.Formatter(log_format))
logging.getLogger().addHandler(fh)

```

# argparse

```python	
import argparse
parser = argparse.ArgumentParser("")
parser.add_argument('--batch_size', type=int, default=64, help='batch size')
parser.add_argument('--learning_rate', type=float, default=0.025, help='init learning rate')
parser.add_argument('--cutout', action='store_true', default=False, help='use cutout')
args = parser.parser_args()
args.batch_size
```

