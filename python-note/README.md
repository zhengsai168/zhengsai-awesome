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
```

