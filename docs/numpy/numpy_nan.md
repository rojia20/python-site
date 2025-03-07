# Numpy - All About NaN

## 前言
- NaN 表示 not a number 
- 出现 NaN的情景：
    1. 0/0
    2. data is missing
    3. data type （dtype）is float
    4. inappropriate calculation
        - eg. (infinity - infinity)
- np.nan 与 np.nan 不相等
    - np.nan == np.nan --> output: False
    - np.nan != np.nan --> output: True

## Import Modules
```
import numpy as np
```

## Data Source
- create an array with the data point (3, 3) is NaN
```
Create an array: 
t1 = np.arange(24).reshape(4, 6)

Assign data point (3,3) to NaN:
t4 = t1.astype(float)
t4[3, 3] = np.nan 
```

## Functions
### 1. 判断 array（数组）中 NaN 个数 
- 利用 NaN 特性
- 例： count numbers of NaN in t4
```
方法1:

np.count_nonzero(t4 != t4)

# 因为只有 NaN 时 t4 != t4 为 True （= 1），其他为 False
```
```
方法2: 

np.count_nonzero(np.isnan(t4))
```

### 2. 判断当前数组中哪个数值为 NaN
- 利用 NaN 特性
```
方法1:

np.isnan(t4)

# output：dtype = bool （In this example, it is a bool array)
```
```
方法2: 

print(t4 != t4)
```

### 3. NaN 有关的计算 
- NaN 和任何值计算，结果都为 NaN

#### Demo 1 
```
np.sum(t4)

# output = NaN
```
```
np.sum(t4,axis = 0)

# output = [ 0. 40. 44. nan 52. 56.]
```

#### Demo 2:
- 指定求哪个方向的和 - using axis
```
Create a new array:

t5 = np.arange(12).reshape(3, 4)
```
```
求每一列的和 (column total):

np.sum(t5, axis = 0)

# shape of output is as same as each row 
```
```
求每一行的和 (row total):

np.sum(t5, axis = 1)

# shape of output is as same as each column
```

### 4. 处理 NaN 的操作
#### 方法 1
- 用该列/行的均值 (or median) 替换 NaN 
    - depends on whether we looking for column or row total

#### 方法 2 (not recommended)
- 直接删除有缺失值的那一行 
    - 因为一行被视为一条数据




## 拓展: 判断 array（数组）中 非零数的个数 
- Count numbers of nonzero in t4
```
t4[:,0] = 0

np.count_nonzero(t4)
```