# Numpy - Read Data

## 前言
- 读取数据一般不用numpy，而是pandas
    - pandas更强大
- Data file的格式通常是CSV file (Comma-Separated Value)
    - 基本语法：`np.loadtxt(fname, dtype = np.float, delimiter = None, skiprows = 0, usecols = None, unpack = False)`
    - `delimiter` --> 分隔字符串: 默认为空格，可改为逗号
    - `skiprows` --> 跳过前X行
    - `usecols` --> 读取指定的列
    - `unpack` --> 转制: 将行转成列，将列转成行。 默认 unpack = False

## Import Modules
```python
import numpy as np
```

## Data Source
```python
# Read CSV file
us_file_path = "./data/us_videos.csv"
uk_file_path = "./data/gb_videos.csv"

us = np.loadtxt(us_file_path, delimiter = ",", dtype = "int", skiprows = 1)
uk = np.loadtxt(uk_file_path, delimiter = ",", dtype = "int", skiprows = 1)
```
```python
# 自建数组
t1 = np.arange(24).reshape(4, 6)
print(t1)
```

## Functions
### 1. Transpose （转制）
```python
# 方法1:

t1.transpose()
```

```python
# 方法2：

t1.T
```

### 2. Extract row and/or columns
- 基本语法：`data[rows, columns]`

#### 2.1 Extract one row
```python
# Extract the third row:

us[2]
```
```python
# An alternative way:

us[2, :]
```

#### 2.2 Extract mutiple rows 
```python
# Extract second and thrid rows：

us[1:3]
```
```python
# Extract every row after the thrid row：

us[2:]
```
```python
# Extract multiple but inconsistant rows：

us[[2, 8, 10]]
```

#### 2.3 Extract one column
```python
# Extract the thrid column:

us[:, 2]

# :表示对rows不做特别处理
```

#### 2.4 Extract multiple columns
```python
# Extracting the second and third columns:

us[:, 1:3]
```
```python
# Extract every column after the thrid column:

us[:, 2:]
```
```python
# Extract multiple but inconsistant columns:

us[:, [0, 1, 3]]
```

#### 2.5 Extract one row and one column 
- This is equivalent to extracting a data point

```python
us[2, 3] 
```

#### 2.6 Extract multiple rows and multiple columns (continuous)
```python
us[2:5, 1:4]
```

#### 2.7 Extract multiple rows and multiple columns (inconsistant) 
- This is equivalent to extracting mutiple data points

```python
# 取 matrix（数阵）中不相邻的两个点:

us[[0, 2], [0, 1]] 

# 点坐标: 第一行第三列（0， 2），第一行第二列 （0， 1）
```

### 3. 取步长
- 例：`[:2]`

```python
# 每两列一取值：

us[:, 2::2]

# :2 表示 step == 2 
```
```python
# Star from the second column, and step is 2 (including the fourth column):

us[:, 1::2]
```

### 4. Manipulating Data

#### 4.1 Manipulate data points all at once
```python
# Original data: 

us[1,1:4]
```
```python
# Assign 0 to all: 

us[1,1:4] = 0 
```

#### 4.2 Manipulate data points with conditions

#### 4.2.1 Manipulate data points that are less than or equal to 10:
```python
t1[t1 <= 10] = 3
```

 - *原理:*  
    - *`t1 < 10` gives an output that has a dtype = bool (True or False)*                  
    - *`t1[t1 <= 10] = 3` --> 将 t1 matrix 中 True 的位置统统替换为 3*      

#### 4.2.2 Replace t1 < 10 with 0 and t1 > 10 with 10 
- 一个临界点

```python
np.where(t1 < 10, 0, 10)
```

- *解析: if t1 < 10, then t1 = 0, otherwise t1 = 10*

#### 4.2.3 Replace t1 < 10 with 10 and t1 > 18 with 18 
- 两个临界点

```python
# 用 clip 裁剪:

t1.clip(10, 18)
```

### 5. 赋值 NaN 
- data must be float before converting to NaN

```python
# 赋值 data point (3, 3) with NaN:

t4 = t1.astype(float)
t4[3, 3] = np.nan 
```

## Footnotes
- Using a divider when coding can achieve better visualization and clarity 

- Example:

```python
print("*"*100)
```
