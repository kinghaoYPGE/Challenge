## Numpy common methods

NumPy 的主要对象是多维数组 Ndarray。

在 NumPy 中维度（dimensions）叫做轴（**axes**），轴的个数叫做秩（**rank**）。

## array define

### 1. array

use array to new matrices

```
np.array([1,2,3]) #创建一维数组rank=1, axes=3
np.array([(1,2,3),(4,5,6)]) #创建二维数组rank=2, axes=3

```

### 2. zeros

创建全为 0 的二维数组

```
np.zeros((2,3))
out: array([[0., 0., 0.],        	
        	[0., 0., 0.]])	
```

### 3. ones

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

### 4. arange

```
np.arange(5) #创建一维等差数组
out: array([0, 1, 2, 3, 4])

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

### 4. eye

```
np.eye(3) #创建单位矩阵（二维数组）
out: array([[1., 0., 0.],
       		[0., 1., 0.],
       		[0., 0., 1.]])
```

### 5. linspace

```
np.linspace(1, 10, num=6) #创建等间隔一维数组
out: array([ 1. ,  2.8,  4.6,  6.4,  8.2, 10. ])
```

### 6. random.rand

```
np.random.rand(2,3) #创建二维随机数组
out: array([[0.50122984, 0.98824375, 0.81388012],
       	   [0.60951775, 0.02055326, 0.97622093]])
```

### 7. random.randint

```
np.random.randint(5, size=(2,3)) #创建二维随机整数数组（数值小于 5）
out: array([[2, 0, 2],
       		[4, 4, 4]])
```

### 8. fromfunction

usage: np.fromfunction(function, (size))

```
np.fromfunction(lambda i, j: i + j, (3, 3)) #依据自定义函数创建数组
out: array([[0., 1., 2.],
       		[1., 2., 3.],
       		[2., 3., 4.]])
```

## array calculation

