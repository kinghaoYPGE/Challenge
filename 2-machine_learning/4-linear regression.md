### 1. Data Pre-Processing

#### Step 1: Importing the required Libraries

```
import numpy as np
import pandas as pd
```



#### Step 2: Importing the Data Set

```
dataFrame = pd.read_csv('test.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : , 3].values
```



#### Step 3: Handling the Missing Data

replace the missing data by the Mean or Median of the entire column.

```
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = "NaN", strategy = "mean", axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
```

#### Step 4: Encoding Categorical Data

We need to encode these variables like 'Yes' or 'No' into numbers

```
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])

#Creating a dummy variable
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_Y = LabelEncoder()
Y =  labelencoder_Y.fit_transform(Y)
```



#### Step 5: Splitting the dataset into test set and training set

We make two partitions of dataset one for training set and other for testing set

The split is generally 80/20. 

```
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X , Y , test_size = 0.2, random_state = 0)
```



#### Step 6: Feature Scaling

Done by Feature standardization or Z-score normalization

```
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.fit_transform(X_test)
```

### 2. Simple Linear Regression

#### Step 1: Pre-Process the data

as above.

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

dataset = pd.read_csv('studentscores.csv')
X = dataset.iloc[ : ,   : 1 ].values
Y = dataset.iloc[ : , 1 ].values

from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split( X, Y, test_size = 1/4, random_state = 0) 
```

#### Step 2: Fitting model to the training set

```
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor = regressor.fit(X_train, Y_train)
```

#### Step 3: Predicting the result

We will predict the observations from test set. 

We will save the output in a vector Y_pred

```
Y_pred = regressor.predict(X_test)
```

#### Step 4: Visualization

Make Scatter Plots of Training set results and Test set results

to see how close our model predicted the values

```
# Visualising the Training results
plt.scatter(X_train , Y_train, color = 'red')
plt.plot(X_train , regressor.predict(X_train), color ='blue')

# Visualizing the test results
plt.scatter(X_test , Y_test, color = 'red')
plt.plot(X_test , regressor.predict(X_test), color ='blue')
```



### 3. Multiple Linear Regression

We can find out which factor has the highest impact on the predicted output and how different variables relate to each other

#### Step 1: Data Preprocessing

```
#Importing the libraries
import pandas as pd
import numpy as np

#Importing the dataSet
dataset = pd.read_csv('50_Startups.csv')
X = dataset.iloc[ : , :-1].values
Y = dataset.iloc[ : ,  4 ].values

#Encoding Categorical data
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder = LabelEncoder()
X[: , 3] = labelencoder.fit_transform(X[ : , 3])
onehotencoder = OneHotEncoder(categorical_features = [3])
X = onehotencoder.fit_transform(X).toarray()

#Avoiding Dummy Variable Trap
X = X[:, 1:]

#Splitting the dataset into the Training set and Test set
from sklearn.cross_validation import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size = 0.2, random_state = 0)
```

#### Step 2: Fitting Multiple Linear Regression to the Training set

```
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, Y_train)
```

#### Step 3: Predicting the Test set results

```
y_pred = regressor.predict(X_test)
```

### 4. 实战

#### 实战 1-对股票数据进行分析预测

- [ ] https://www.shiyanlou.com/courses/1145

##### 1. 数据来源

1. 雅虎财经
2. Python Quandl 模块

```
import quandl
quandl.get('WIKI/AAPL')
```

1. Pandas Datareader 模块

```
import pandas_datareader.data as web
import datetime
#start = datetime.datetime(2018, 1, 1)
end = datetime.datetime.now()
start = 10 * datatime.timedelta(days=365)
df = web.DataReader('000001.SZ', 'yahoo', start, end)
```

##### 2. 数据预处理

1. 缺失值处理

```
# 判断是否有缺失值
df.isnull().values.sum()
```

2. 数据可视化

```
# pandas的dataframe自带一些画图的方法，也是基于matplotlib
df['Close'].plot(figsize=(16, 9))
```

