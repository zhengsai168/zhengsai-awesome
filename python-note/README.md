# 具名元组 | namedtuple

```python
from collections import namedtuple
city = namedtuple('city','x y z') # 'x y z'可以是可迭代的字符串对象 如 ['x','y','z'] 
city_inst = city(1,2,3)
city_inst.x   # 等价于city_inst[0]
city_inst.y
city_inst.z
```

