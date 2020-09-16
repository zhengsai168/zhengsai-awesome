# 创建数组

```
Numpy 常用基本数据类型：
bool,int8,16,32,64,float16,32,64
```

```python
import numpy as np

np.array([1,2,3],dtype=np.float64)

# 0填充
np.zeros(10,dtype=np.int64)

# 1填充
np.ones((3,3),dtype=np.float64)

# 任意数值填充
np.full((2,2),3.14)

# 类似range的填充
np.arange(0,20,2)

# 包括首尾的平均切分
np.linspace(0,1,5)

# 设置numpy随机种子
np.random.seed(0)

# 0~1 均匀分布
np.random.random((3,3))

# 0~2均匀分布
np.random.uniform(0,2,(3,3))

# mean=0,std=1 正态分布
np.random.normal(0,1,(2,2))

np.random.randint(0,10,(2,2))

# 单位矩阵I
np.eye(3)
```

# 数组属性

```python	
x = np.random.random((3,4,5))

# 维数
x.ndim

# 每一维的大小
x.shape

# 总大小
x.size

# 数据类型
x.dtype

# 按字节的大小（一个数和整个数组的）
x.itemsize  #单个数
x.nbytes  #整个数组
```

# 切片索引

```python
x[0][1][1]

x[0,1,2]

x[:4]

x[::2,::2,::2]

x[0,:,:]

y = x[0,:,:].copy()
```

# 变形

```python
# 变形
x = np.arange(9).reshape((3,3))

# 增加一维
x = x[np.newaxis,:]
```

# 拼接和分裂

```python
x=np.array([1,2,3])
y=np.array([3,2,1])
np.concatenate([x,y])

z = np.array([3,5,6])
np.concatenate([x,y,z])

# 按0维度拼接
grid = np.arange(6).reshape((2,3))
np.concatenate([grid,grid])

# 按1维度拼接
np.concatenate([grid,grid],axis=1)

# 垂直拼接 （即按0维度）
np.vstack([grid,grid])

# 水平拼接 (即按1维度)
np.hstack([grid,grid])

# 分裂
x = np.arange(9)
x1,x2,x3 = np.split(x,[3,5])

# 垂直分裂
x = np.arange(16).reshape((4,4))
x1,x2 = np.vsplit(x,[2])

# 水平分裂
x1,x2 = np.hsplit(x,[2])
```

# 通用函数

```python
x = np.arange(4)

x*2

x/2

x//2

2**x

x+2

abs(x-2)

np.abs(x-2)

x = np.linspace(0,np.pi,3)

np.sin(x)

x = [-1,0,1]
np.arcsin(x)

np.log  

np.log2

np.log10

np.exp
```

# 聚合

```python
x = np.arange(1,6)
np.add.reduce(x)

np.add.accumulate(x)

np.multiply.reduce(x)

np.sum(x)

x.sum()
```

### 聚合函数

```python
sum  nannum  # 有nan的是NaN安全版本
prod # 乘积
mean # 均值
std # 标准差
var # 方差
min
max
argmin # 索引
argmax 
median
any
all

x = np.random.randint(0,10,6).reshape(2,3)
x.argmin()
```

# 广播

```python
a = np.arange(3)
b = np.arange(3)
a+b

a+3

a = np.arange(3)
b = np.arange(6).reshape(2,3)
a+b

a = np.arange(3).reshape(1,3)
b = np.arange(3).reshape(3,1)
a+b

y = np.array(x>3,dtype=np.int64)

ind = [(0,0),(0,2)]
y[ind]
```

