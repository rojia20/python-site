# Pandas - DataFrame

## 前言
- Dataframe is two dimensional 
  
## Import Modules
```python
import pandas as pd 
import numpy as np
from pymongo import MongoClient
```

## Functions
### 1. Create a DataFrame
```python
df = pd.DataFrame(np.arange(12).reshape(3, 4))

# Output: 0  1   2   3 --> this is column index -- called columns, axis = 1
     # 0  0  1   2   3
     # 1  4  5   6   7
     # 2  8  9  10  11
     # |
# this is row index -- called index, axis = 0
```
### 2. Create a DataFrame: self-define index and columns 
```python
df_1 = pd.DataFrame(np.arange(12).reshape(3, 4), index = list("abc"), columns = list("wxyz"))
```

### 3. Create a dataframe: using dictionary 
```python
d1 = {"name":["xiaoming", "xiaowang"], "age":[20, 32], "tel":[10086, 10010]}

df_2 = pd.DataFrame(d1)
```
```python
d2 = [{"name":"xiaoming", "age":20, "tel":10086}, {"name":"xiaowang", "age":32, "tel":10010}, {"name":"xiaohe", "age":22, "tel":10099}]

df_3 = pd.DataFrame(d2)
```
```python
d3 = [{"name":"xiaoming", "age":20, "tel":10086}, {"name":"xiaowang", "age":32, "tel":10010}, {"name":"xiaohe", "age":22}]

df_4 = pd.DataFrame(d3)

print(df_4) # Output: 没有传值的地方会显示NaN
```

### 4.  Features in DataFrame
#### 1. Check index (row index)
```python
df_2.index
```

#### 2. Check columns (column index)
```python
df_2.columns
```

#### 3. Check values (values only)
```python
df_2.values 
# ndarray
```
#### 4. Check the shape of dataframe
```python
df_2.shape
```

#### 5. Check data type of values (for each column) in dataframe
```python
df_2.dtypes
```
#### 6. Check the dimension of dataframe
```python
df_2.ndim
```
#### 7. Show the first few rows
```python
df_2.head

# Default: the first five rows 
```
```python
df_2.head(1) # show the first row
```

#### 8. Show the last few rows
```python
print(df_2.tail)

# default: the last five rows 
```
```python
df_2.tail(2) # show the second to last row
```

#### 9. Present the description for a datframe 
```python
df_2.info()
```
#### 10. Present statistical description of a dataframe (mean, SD, min, max, median, first and thrid quartile)
```python
df_2.describe()

# Only for data type == int or float 
```

