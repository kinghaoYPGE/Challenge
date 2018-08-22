## Numpy common methods

NumPy 的主要对象是多维数组 Ndarray。

在 NumPy 中维度（dimensions）叫做轴（**axes**），轴的个数叫做秩（**rank**）。

## array define

### 1. array -创建数组

use array to new matrices

```
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
np.arange(1, 6) #创建一维等差数组，以1开始
out: array([0, 1, 2, 3, 4])
	 array([1, 2, 3, 4, 5]))

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

```
np.linspace(1, 10, num=6) #创建等间隔一维数组
out: array([ 1. ,  2.8,  4.6,  6.4,  8.2, 10. ])
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

## array calculation

### 1. 一维数组乘法运算

```
a = np.array([10,20,30,40,50]) #array([10, 20, 30, 40, 50])
b = np.arange(1,6) #array([1, 2, 3, 4, 5])

a * b #一维数组乘法运算
out: array([ 10,  40,  90, 160, 250])

```

### 2. 矩阵`元素间`乘法运算

```
A = np.array([[1,2,3],[4,5,6]]) #array([[1, 2, 3],
									[4, 5, 6]])
B = np.array([[3,2,1],[6,5,4]]) # array([[3, 2, 1],
									[6, 5, 4]]))
#矩阵元素间乘法运算就是每个元素相乘								     						out: array([[ 3,  4,  3],
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

