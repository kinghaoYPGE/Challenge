# Pandas

Pandas 是基于 NumPy 的一种**数据处理工具**，该工具为了解决数据分析任务而创建 。

Pandas 的数据结构：Pandas 主要有 **Series**（一维数组），**DataFrame**（二维数组），Panel（三维数组），Panel4D（四维数组），PanelND（更多维数组）等数据结构。其中 Series 和 DataFrame 应用的最为广泛。 

Series 是一维**带标签**的数组，它可以包含任何数据类型。包括整数，字符串，浮点数，**Python 对象**等。Series 可以通过标签来定位。
DataFrame 是二维的**带标签**的数据结构。我们可以通过标签来定位数据。这是 NumPy 所没有的。

## 1. 数据类型

 ### 1. Series

#### 1.创建Series

1. **从列表创建 Series**

pd.Series(arr, index=index)

```
arr=[0, 1, 2, 3, 4]
s1=pd.Series(arr) # 如果不指定索引，则默认从 0 开始
s1
out:
0    0
1    1
2    2
3    3
4    4
dtype: int64
```

2.  **从 Ndarray 创建 Series**

```
import numpy as np
n=np.random.randn(5) # 创建一个随机 Ndarray 数组

index=['a','b','c','d','e']
s2=pd.Series(n,index=index)
s2
out:
a   -0.483267
b    0.692403
c   -1.097971
d    0.177133
e    0.323855
dtype: float64
```

3.**从字典创建Series**

```
d={'a':1,'b':2,'c':3,'d':4,'e':5}
s3=pd.Series(d)
s3
out:
a    1
b    2
c    3
d    4
e    5
dtype: int64
```

#### 2.Series基本操作

```
s1.index=['A','B','C','D','E'] # 修改后的索引
s1
out:
A    0
B    1
C    2
D    3
E    4
dtype: int64

s4=s3.append(s1) # 将 s1 拼接到 s3
s4
out:
a    1
b    2
c    3
d    4
e    5
A    0
B    1
C    2
D    3
E    4
dtype: int64

s4=s4.drop('e') # 删除索引为 e 的值
s4
out:
a    1
b    2
c    3
d    4
A    0
B    1
C    2
D    3
E    4
dtype: int64

s4['A']=6 # 修改索引为 A 的值 = 6
s4
out:
a    1
b    2
c    3
d    4
A    6
B    1
C    2
D    3
E    4
dtype: int64

s4['B'] #Series 按指定索引查找元素
out: 1

s4[:3] #Series切片
out:
a    1
b    2
c    3
dtype: int64
```

#### 3.Series运算

1. **Series加法/减法运算**

Series 的加法/减法运算是按照索引计算，如果索引不同则填充为 `NaN`（空值）。 

```
s4.add(s3)
out:
A    NaN
B    NaN
C    NaN
D    NaN
E    NaN
a    2.0
b    4.0
c    6.0
d    8.0
e    NaN
dtype: float64

s4.sub(s3)
out:
A    NaN
B    NaN
C    NaN
D    NaN
E    NaN
a    0.0
b    0.0
c    0.0
d    0.0
e    NaN
dtype: float64
```

2. **Series乘法/除法运算**

Series 的乘法/除法运算是按照索引对应计算，如果索引不同则填充为 `NaN`（空值）。 

```
s4.mul(s3)
out:
A     NaN
B     NaN
C     NaN
D     NaN
E     NaN
a     1.0
b     4.0
c     9.0
d    16.0
e     NaN
dtype: float64

s4.div(s3)
out:
A    NaN
B    NaN
C    NaN
D    NaN
E    NaN
a    1.0
b    1.0
c    1.0
d    1.0
e    NaN
dtype: float64
```

3. **Series 求中位数/求和/求最大值/求最小值**

```
s4.median()
out: 3.0

s4.sum()
out: 26

s4.max()
out: 6

s4.min()
out: 1
```

### 2. DataFrame

与 Sereis 不同，DataFrame 可以存在多列数据。一般情况下，DataFrame 也更加常用。 

#### 1. 创建DataFrame

1. **通过 NumPy 数组创建 DataFrame**

```
dates=pd.date_range('today',periods=6) # 定义时间序列作为 index
num_arr=np.random.randn(6,4) # 传入 numpy 随机数组
columns=['A','B','C','D'] # 将列表作为列名
df1=pd.DataFrame(num_arr,index=dates,columns=columns)
df1
out:
							A			B			C			D
2018-04-17 01:12:38.805877	0.848962	-0.377572	2.124144	0.794958
2018-04-18 01:12:38.805877	-0.920862	0.201444	-0.590866	0.902380
2018-04-19 01:12:38.805877	0.965119	0.016123	-0.799221	0.345228
2018-04-20 01:12:38.805877	-0.339873	-0.580011	-0.337110	-1.262724
2018-04-21 01:12:38.805877	-0.184359	0.215222	-0.878790	-0.216809
2018-04-22 01:12:38.805877	-0.223707	-0.179329	-0.794284	-1.555711
```

2. **通过字典数组创建 DataFrame**

```
data = {'animal': ['cat', 'cat', 'snake', 'dog', 'dog', 'cat', 'snake', 'cat', 'dog', 'dog'],
        'age': [2.5, 3, 0.5, np.nan, 5, 2, 4.5, np.nan, 7, 3],
        'visits': [1, 3, 2, 3, 2, 3, 1, 1, 2, 1],
        'priority': ['yes', 'yes', 'no', 'yes', 'no', 'no', 'no', 'yes', 'no', 'no']}

labels = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
df2 = pd.DataFrame(data, index=labels)
df2
out:
	age	animal	priority	visits
a	2.5	cat		yes			1	
b	3.0	cat		yes			3
c	0.5	snake	no			2
d	NaN	dog		yes			3
e	5.0	dog		no			2
f	2.0	cat		no			3
g	4.5	snake	no			1
h	NaN	cat		yes			1
i	7.0	dog		no			2
j	3.0	dog		no			1
```

3. **查看 DataFrame 的数据类型**

```
df2.dtypes
out:
age         float64
animal       object
priority     object
visits        int64
dtype: object
```

#### 2. DataFrame基本操作

```
df2.head() # 默认为显示 5 行，可根据需要在括号中填入希望预览的行数
df2.tail(3) # 显示后三行数据
df2.index #查看 DataFrame 的索引
df2.columns #查看 DataFrame 的列名
df2.values 查看 DataFrame 的数值
out: 
array([[2.5, 'cat', 'yes', 1],
       [3.0, 'cat', 'yes', 3],
       [0.5, 'snake', 'no', 2],
       [nan, 'dog', 'yes', 3],
       [5.0, 'dog', 'no', 2],
       [2.0, 'cat', 'no', 3],
       [4.5, 'snake', 'no', 1],
       [nan, 'cat', 'yes', 1],
       [7.0, 'dog', 'no', 2],
       [3.0, 'dog', 'no', 1]], dtype=object)
       
df2.describe() #查看 DataFrame 的统计数据
out:
		age			visits
count	8.000000	10.000000
mean	3.437500	1.900000
std		2.007797	0.875595
min		0.500000	1.000000
25%		2.375000	1.000000
50%		3.000000	2.000000
75%		4.625000	2.750000
max		7.000000	3.000000

df2.T #DataFrame 转置操作
out:
			a	b	c	d	e	f	g	h	i	j
age			2.5	3	0.5	NaN	5	2	4.5	NaN	7	3
animal		cat	cat	snake	dog	dog	cat	snake	cat	dog	dog
priority	yes	yes	no	yes	no	no	no	yes	no	no
visits		1	3	2	3	2	3	1	1	2	1

df2.sort_values(by='age') # 对 DataFrame 进行按列排序, 按 age 升序排列
df2[1:3] # 对 DataFrame 数据切片
out:
	age	animal	priority	visits
b	3.0	cat		yes			3
c	0.5	snake	no			2

df2['age']/df2.age # 对 DataFrame 通过标签查询（单列）
out:
a    2.5
b    3.0
c    0.5
d    NaN
e    5.0
f    2.0
g    4.5
h    NaN
i    7.0
j    3.0
Name: age, dtype: float64

df2[['age','animal']] # 对 DataFrame 通过标签查询（多列), 传入一个列名组成的列表

df2.iloc[1:3] #  对 DataFrame 通过位置查询, 查询 2，3 行
out:
	age	animal	priority	visits
b	3.0	cat		yes			3
c	0.5	snake	no			2

df3=df2.copy() # 生成 DataFrame 副本，方便数据集被多个不同流程使用

df3.isnull() # 如果为空则返回为 True

num=pd.Series([0,1,2,3,4,5,6,7,8,9],index=df3.index)
df3['No.']=num # 添加列数据, 添加以 'No.' 为列名的新数据列
df3
out:
	age	animal	priority	visits	No.
a	2.5	cat		yes			1		0
b	3.0	cat		yes			3		1
c	0.5	snake	no			2		2
d	NaN	dog		yes			3		3
e	5.0	dog		no			2		4
f	2.0	cat		no			3		5
g	4.5	snake	no			1		6
h	NaN	cat		yes			1		7
i	7.0	dog		no			2		8
j	3.0	dog		no			1		9


df3.iat[1,0]=2 # 修改第 2 行与第 1 列对应的值 3.0 → 2.0, 索引序号从 0 开始，这里为 1, 0

df3.loc['f','age']=1.5 # 根据 DataFrame 的标签对数据进行修改

df3.mean() # DataFrame 求平均值操作
out:
age       3.25
visits    1.90
No.       4.50
dtype: float64

df3['visits'].sum() # 对 DataFrame 中任意列做求和操作
```

#### 3. 字符串操作

```
string = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])
print(string)
string.str.lower() # 将字符串转化为小写字母
string.str.upper() # 将字符串转化为大写字母
```

#### 4. DataFrame缺失值操作

```
df4=df3.copy()
print(df4)
df4.fillna(value=3) # 对缺失值进行填充

df5=df3.copy()
print(df5)
df5.dropna(how='any') # 删除缺失值的行, 任何存在 NaN 的行都将被删除

left = pd.DataFrame({'key': ['foo1', 'foo2'], 'one': [1, 2]})
right = pd.DataFrame({'key': ['foo2', 'foo3'], 'two': [4, 5]})
print(left)
print(right)
# 按照 key 列对齐连接，只存在 foo2 相同，所以最后变成一行
pd.merge(left, right, on='key')
left:
    key  one
0  foo1    1
1  foo2    2
right:
    key  two
0  foo2    4
1  foo3    5

	key		one	two
0	foo2	2	4
```

#### 5. DataFrame文件操作

##### 1. csv文件写入/读取

```
df3.to_csv('animal.csv')
df_animal=pd.read_csv('animal.csv')
```

##### 2. Excel文件写入/读取

```
df3.to_excel('animal.xlsx', sheet_name='Sheet1')
pd.read_excel('animal.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
```

