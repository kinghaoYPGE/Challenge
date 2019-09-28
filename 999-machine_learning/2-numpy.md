## Numpy common methods

NumPy 的主要对象是多维数组 Ndarray。

在 NumPy 中维度（dimensions）叫做轴（**axes**），轴的个数叫做秩（**rank**）。

## Array define

### 1. array -创建数组

use array to new matrices

```python
np.array([1,2,3]) #创建一维数组rank=1, axes=3
np.array([(1,2,3),(4,5,6)]) #创建二维数组rank=2, axes=3

```

### 2. zeros -创建`元素为0`的数组

创建全为 0 的二维数组

```
np.zeros((2,3))
out: array([[0., 0., 0.],        	
        	[0., 0., 0.]])	
```

### 3. ones -创建`元素为1`的数组

创建全为 1 的三维数组

```
np.ones((2,3,4))
out: array([[[1., 1., 1., 1.],
        	[1., 1., 1., 1.],
        	[1., 1., 1., 1.]],

       		[[1., 1., 1., 1.],
        	[1., 1., 1., 1.],
        	[1., 1., 1., 1.]]])
```

### 4. arange -创建`等差`数组

```
np.arange(5) #创建一维等差数组
out: array([0, 1, 2, 3, 4])
np.arange(1, 6) #创建一维等差数组，以1开始
out: array([1, 2, 3, 4, 5]))
np.arange(1, 6, 2) #创建一维等差数组，间隔为2

np.arange(6).reshape(2,3) #创建二维等差数组
out: array([[0, 1, 2],
       		[3, 4, 5]])	
np.arange(27).reshape(3,3,3) #创建三维等差数组
out: array([[[ 0,  1,  2],
        	[ 3,  4,  5],
        	[ 6,  7,  8]],

       		[[ 9, 10, 11],
        	[12, 13, 14],
        	[15, 16, 17]],

       		[[18, 19, 20],
        	[21, 22, 23],
        	[24, 25, 26]]])
```

### 4. eye -创建`单位矩阵`

```
np.eye(3) #创建单位矩阵（二维数组）
out: array([[1., 0., 0.],
       		[0., 1., 0.],
       		[0., 0., 1.]])
```

### 5. linspace -创建`等间隔数组`

#### 1. 和arange的区别

> arange()类似于内置函数range()，通过指定开始值、终值和步长创建表示等差数列的一维数组，注意得到的结果数组不包含终值。
>
> linspace()通过指定开始值、终值和元素个数创建表示等差数列的一维数组，可以通过endpoint参数指定是否包含终值，默认值为True，即包含终值。

```
np.linspace(1, 10, num=6) #创建等间隔一维数组
out: array([ 1. ,  2.8,  4.6,  6.4,  8.2, 10. ])

# 注意linspace中endpoint参数
np.linspace(0, 10,num=10, dtype='int32', endpoint=True)
out: array([ 0,  1,  2,  3,  4,  5,  6,  7,  8, 10], dtype=int32)

np.linspace(0, 10,num=10, dtype='int32', endpoint=False)
out: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], dtype=int32)
```

### 6. random.rand -创建`随机数组`

```
np.random.rand(2,3) #创建二维随机数组
out: array([[0.50122984, 0.98824375, 0.81388012],
       	   [0.60951775, 0.02055326, 0.97622093]])
```

### 7. random.randint -创建`随机整数组`

```
np.random.randint(5, size=(2,3)) #创建二维随机整数数组（数值小于 5）
out: array([[2, 0, 2],
       		[4, 4, 4]])
```

### 8. fromfunction -`自定义`矩阵

usage: np.fromfunction(function, (size))

```
np.fromfunction(lambda i, j: i + j, (3, 3)) #依据自定义函数创建数组
out: array([[0., 1., 2.],
       		[1., 2., 3.],
       		[2., 3., 4.]])
```



### 9. 从已知数据创建

1. `frombuffer（buffer）`：将缓冲区转换为 `1` 维数组。
2. `fromfile（file，dtype，count，sep）`：从文本或二进制文件中构建多维数组。
3. `fromfunction（function，shape）`：通过函数返回值来创建多维数组。
4. `fromiter（iterable，dtype，count）`：从可迭代对象创建 `1` 维数组。
5. `fromstring（string，dtype，count，sep）`：从字符串中创建 `1` 维数组。

### 10. ndarry其他属性



```
b = np.array([[1,2,3],[4,5,6],[7,8,9]])
b.imag  	# ndarray.imag 用来输出数组包含元素的虚部。 
out: array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]])
b.real 		# ndarray.real用来输出数组包含元素的实部。
out: array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
b.size		# ndarray.size用来输出数组中的总包含元素数。  
out: 9
```



## array/matrix calculation

矩阵和数组在python中的运算是不一样的，但是可以互相转换

### 1. 一维数组乘法运算

```
a = np.array([10,20,30,40,50]) #array([10, 20, 30, 40, 50])
b = np.arange(1,6) #array([1, 2, 3, 4, 5])

a * b #一维数组乘法运算
out: array([ 10,  40,  90, 160, 250])

```

### 2. 数组`元素间`乘法运算

```
A = np.array([[1,2,3],[4,5,6]]) #array([[1, 2, 3],
									[4, 5, 6]])
B = np.array([[3,2,1],[6,5,4]]) # array([[3, 2, 1],
									[6, 5, 4]]))
#矩阵元素间乘法运算就是每个元素相乘	
out: array([[ 3,  4,  3],
       		[24, 25, 24]])								     
```

### 3.  dot/(mat(A)*mat(B))	-矩阵乘法运算

```
np.dot(A, B) #需满足等式 m,n = n,m
#A = (2,3), B = (2,3) -ValueError: shapes (2,3) and (2,3) not aligned: 3 (dim 1) != 2 (dim 0)
#重新定义, A=(2,2), B=(2,2)--> C=(2,2)
A = np.array([[1,2],
           [3,4]])
B = np.array([[5,6],
           [7,8]])
np.dot(A, B)            
out:array([[19, 22],
       	  [43, 50]])
# 如果使用 np.mat 将二维数组准确定义为矩阵，就可以直接使用 * 完成矩阵乘法计算
np.mat(A) * np.mat(B)
out: matrix([[19, 22],
        	[43, 50]])
       	  
```

### 4. 矩阵的`转置`(A->A.T)

```
A.T
out:array([[1, 3],
       	[2, 4]])
```

### 5. linalg.inv -矩阵`求逆`(A->1/A)

```
#这里要注意必须是方阵才可以求逆
np.linalg.inv(A)
out: array([[-2. ,  1. ],
       		[ 1.5, -0.5]])
```

## 数组/矩阵切片和索引

### 1.一维数组索引/切片

```
a = np.array([1, 2, 3, 4, 5])
a[0], a[-1]
out: (1, 5)

a[0:2], a[:-1]
out: (array([1, 2]), array([1, 2, 3, 4]))
```

###2. 二维数组索引/切片

```
a = np.array([(1,2,3),(4,5,6),(7,8,9)])
a[0], a[-1]
out: (array([1, 2, 3]), array([7, 8, 9]))

a[:, 1] #取第二列
out: array([2, 5, 8])

a[1:3, :] #取第2, 3行
out: array([[4, 5, 6],
       [7, 8, 9]])
```

### 3.数组形状操作

```
a = np.random.random((3, 2)) #生成二维示例数组
out: array([[0.5041298 , 0.90467466],
       [0.05589025, 0.11222457],
       [0.24464299, 0.17077689]])
a.shape #查看数组形状
out: (3, 2)

a.reshape(2, 3) # 更改数组形状（改变原始数组）
out:array([[0.5041298 , 0.90467466, 0.05589025],
       [0.11222457, 0.24464299, 0.17077689]])
       
a.ravel(order='C') 
#展平数组 order 表示变换时的读取顺序，默认是按照行依次读取，当 order='F' 时，可以按列依次读取排序
out: array([0.5041298 , 0.90467466, 0.05589025, 0.11222457, 0.24464299,
       0.17077689])
       
# 生成示例数组
a = np.random.randint(10, size=(3, 3))
b = np.random.randint(10, size=(3, 3))
a, b
out: (array([[6, 5, 6],
        [1, 3, 2],
        [6, 7, 8]]), array([[2, 6, 1],
        [6, 2, 0],
        [6, 7, 7]]))
        
np.vstack((a, b)) #垂直拼合数组
out: array([[6, 5, 6],
       [1, 3, 2],
       [6, 7, 8],
       [2, 6, 1],
       [6, 2, 0],
       [6, 7, 7]])

np.hstack((a, b)) #水平拼合数组
out: array([[6, 5, 6, 2, 6, 1],
       [1, 3, 2, 6, 2, 0],
       [6, 7, 8, 6, 7, 7]])
       
np.hsplit(a, 3) #沿横轴分割数组
out: [array([[6],
        [1],
        [6]]), array([[5],
        [3],
        [7]]), array([[6],
        [2],
        [8]])]
        
np.vsplit(a, 3) #沿纵轴分割数组        
out: [array([[6, 5, 6]]), array([[1, 3, 2]]), array([[6, 7, 8]])]

```

### 4.数组排序

```
# 生成示例数组
a = np.array(([1,4,3],[6,2,9],[4,7,2]))
a
out: array([[1, 4, 3],
       [6, 2, 9],
       [4, 7, 2]])
       
np.max(a, axis=0) #返回每列最大值
out: array([6, 7, 9])

np.min(a, axis=1) #返回每行最小值
out: array([1, 2, 2])	

np.argmax(a, axis=0) #返回每列最大值索引
out: array([1, 2, 1])

np.argmin(a, axis=1) #返回每行最小值索引
out: array([0, 1, 2])
```

### 5.数组统计

```python
# 生成示例数组
a = np.array(([1,4,3],[6,2,9],[4,7,2]))
a
out: array([[1, 4, 3],
       [6, 2, 9],
       [4, 7, 2]])
       
np.median(a, axis=0) #统计数组各列的中位数
out: array([4., 4., 3.])

np.mean(a, axis=1) #统计数组各行的算术平均值
out: array([2.66666667, 5.66666667, 4.33333333])

np.average(a, axis=0) # 统计数组各列的加权平均值
out: array([3.66666667, 4.33333333, 4.66666667])

np.var(a, axis=1) #统计数组各行的方差
out: array([1.55555556, 8.22222222, 4.22222222])

np.std(a, axis=0) #统计数组各列的标准偏差
out: array([2.05480467, 2.05480467, 3.09120617])

np.sin(a) # 三角函数
np.exp(a) # 指数函数
np.sqrt(a) # 开平方
np.power(a, 3) # 方根运算

```

### 6. 数组取整

https://www.jianshu.com/p/23a9224780e8

### 7. reshape占位符(-1)

```
a = np.array([1,2,3,4,5])
a.shape
out: (5,)
a.reshape(1, -1)
a.shape
out: (1, 5)
```

### 8. np.full

```
a = np.full((3,3), 0) # 相当于zeros
a = np.full((3,3), 1) # 相当于ones
```

### 9. 其他函数

```python
# 获取数组中大于10的元素
a[a>10]

# sum
np.sum(a)
np.sum(a, axis=0)
np.sum(a, axis=1)

# mean
np.mean(a)
np.mean(a, axis=0)
np.mean(a, axis=1)

# uniform
np.random.uniform(3,4) # 产生随机数

# tile
np.tile(a, (1, 2)) # 重复当前元素生成新的数组

# argsort
a.argsort() # 会得到每个元素的下标
a.argsort(axis=0)

# 广播
a = np.array([1,2,3],
            [2,3,4],
            [5,6,7])
b = np.array([1,2,3])
# 想把a的每一行都加上b，直接使用+即可
a + b
```