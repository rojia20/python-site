# Pandas - Index

## Import Modules
```python
import pandas as pd
import string
import numpy as np
```

## Functions
### 1. Create Series
```python
s = pd.Series(np.arange(10))
```
```python
s1 = pd.Series([1, 2, 31, 12, 3, 4])

print(s1) 
# output: 0     1
      #   1     2 
      #   2    31
      #   3    12
      #   4     3
      #   5     4
      #   dtype: int64
# first column is the index (健), and the second column is our data （value，值）
```

### 2. Create Series: through dictionary 
```python
temp_dict = {"name": "xiaohong", "age": 30, "tel": 10086}
s3 = pd.Series(temp_dict)

# output dtype: object (abbraviation: o)
```

### 3. Assign specific index
- The size of series and index must be the same 

```python
s2 = pd.Series([1, 23, 2, 2, 1], index = list("abcde"))
```

#### Practice
- create a string of numbers (0~9), and use uppercase letter (default: starting from A) as index 

```python
a = {string.ascii_uppercase[i]: i for i in range(10)} 
s4 = pd.Series(a)

print(s4) # outpt dtype = int
```
- Reassign different index to the series 

```python
s5 = pd.Series(a, index = list(string.ascii_uppercase[5:15]))

print(s5)   
# Output: F    5.0
        # G    6.0
        # H    7.0
        # I    8.0
        # J    9.0
        # K    NaN
        # L    NaN
        # M    NaN
        # N    NaN
        # O    NaN  
        # outpt dtype = float
        # since the original series has index from A~J, hence index k~o are not correlated with any number, thus NaN
        # NaN 同理numpy中的nan
```
- Change data type (same as numpy)

```python
s6 = s4.astype(float)

print(s6) # outpt dtype = int
```

### 4. Pandas中的切片&索引
#### 4.1 Select a single data point 
```python
s3["age"] 

# select the data with "age" index
```
```python
s3[2] 

# select data at the second row
```
#### 4.2 Select mutiple rows or columns (continuously)
```python
s3[:2]

# select the first two rows: row 0 and row 1
```
#### 4.3 Select mutiple rows or columns (inconsistantly)
```python
s3[[0, 2]]
```
#### 4.4 Select the first and third row 
```python
s3[["age", "tel"]]
```
```python
s4[2:10:2] 

# :2 --> 表示步长 = 2 
# from the third to tenth row, select every two data inclusively (包含row3 和 row10，每两个数一选)
```
#### 4.5 Select rows or columns (index) outside the Series' range 
- Will result in NaN 
- For newer python, will result in "not in index" error
  
### 4.6 布尔索引
```python
s1[s1 > 10]
```
```python
s4[s4 > 10]

# Series([], dtype: int64) --> 表示所选切片为空 --> series中没有 > 10 的data
```

### 5. Extract Series Index
```python
s3.index
```
```python
for i in s3.index:
    print(i)
```

### 6. Check the charateristic of index 
```python
type(s3.index)

# check the index type
```
```python
len(s3.index) 

# output: 3 --> there are three index --> counts of index == 3
```
```python
list(s3.index) 

# convert them into a list
```
```python
list(s3.index)[:2] 

# list out the first two index 
```

### 7. Check Values in Series 
```python
type(s3.values)
 
# type: ndarray
```
```python
print(s3.values)
```

### 8. Where在series的用法 
- 与numpy不同

```python
s1.where(s1 > 10)   

# output: 0     NaN
        # 1     NaN
        # 2    31.0
        # 3    12.0
        # 4     NaN
        # 5     NaN
# values that are less or equal to 10 will become NaN
```
```python
s1.where(s1 > 10, 1) 

# output: 0     1
        # 1     1
        # 2    31
        # 3    12
        # 4     1
        # 5     1
# whenever the value is less or equal to 10, replace it with 1
```

### Footnotes
- ndarry中的很多方法也可用于series （如：argmax， clip）
