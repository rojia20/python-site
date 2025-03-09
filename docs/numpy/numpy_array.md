# Numpy - About Array

## Import Modules
```python
import numpy as np
import random
```

## Functions
### 1. Generate Array
- ```np.array()```
- ```np.arange()```

```python
# 方法1:

t1 = np.array([1, 2, 3])
```
```python
# 方法2: 

t2 = np.array(range(10))
```
```python
# 方法3：快速生成数组

t3 = np.arange(10)
```
```python
# Create an array, starting with 4 and ending with 10 exclusively with step （步长/间隔）equals 2:

t4 = t3 = np.arange(4, 10, 2) 
```

### 2. Data Type
- ```int``` == integer
- ```float``` == with decimals
- ```bool``` == true/false
- ```complex``` == 复数
    - 例：z=a+bi，当z的虚部b＝0时，z为实数；当z的虚部b≠0时，实部a＝0时，z为纯虚数

#### 2.1 Check data type
```python
t3.dtype

# Output: int64 -- numpy中默认模式，跟随电脑位数。
```

#### 2.2 Assign data type
- Why this is important --> 当内存小的时候，可用numpy修改data type从而便于存储

```python
Example: 

t5 = np.array(range(1, 4), dtype = float)

t6 = np.array(range(1, 4), dtype = 'int8')

t7 = np.array(range(1, 4), dtype = 'i2')

t8 = np.array([1, 1, 0, 1, 0, 0], dtype = bool)
```

#### 2.3 Adjust data type (for existing array)
```python
t9 = t5.astype("int8")
```

### 3. Decimals (Fractionals) 
```python
# Generate an array with 10 random frasctionals - using random.random() --> 自动产生一个小数:

t10 = np.array([random.random() for i in range(10)])
```

#### 3.1 Keep certain decimals for each fractional in this array 
```python
# 方法1:

t11 = np.round(t10, 2)
```
```python
# 方法2:

round(random.random(), 3)
```

### 4. Data Shape 
#### 4.1 一维数组
```python
t12 = np.arange(12)

# Check the data shape:
t12.shape

# output: (12,) -- 一维数组 == 原组
```

#### 4.2 二维数组
```python
t13 = np.array([[1, 2, 3], [4, 5, 6]])

t13.shape 

# output: (2, 3) -- (# of rows, # of columns) -- 二维数组
```

#### 4.3 三维数组
```python
t14 = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

t14.shape

# output: (2, 2, 3) -- (# of parts, # of rows, # of columns) -- 三维数组
```

### 5. Reshaping Data 
- ```reshape()```有返回值，不对原array进行修改。不同于```extend```或```update```

#### 5.1 Reshape an existing array from 1D to 2D
```python
t15 = np.arange(12)

t15.reshape((3, 4))
```
#### 5.2 Reshape an existing array from 1D to 3D
```python
t16 = np.arange(24).reshape((2, 3, 4))
```
#### 5.3 Reshape an existing array from 3D to 2D
```python
t16.reshape(4, 6)
```
#### 5.4 Reshape an existing array from 2D to 1D
```python
t16.reshape(24,)
```
#### 5.5 Reshape an unknown shape/size 3D array to 1D
- ```[0]``` == # of parts
- ```[1]``` == # of rows
- ```[2]``` == # of columns

```python
t17 = t16.reshape((t16.shape[0] * t16.shape[1] * t16.shape[2]),) 
```
#### 5.6 Reshape an unknown shape/size 2D array to 1D
- ```[0]``` == # of rows
- ```[1]``` == # of columns

```python
t18 = t16.reshape((t16.shape[0] * t16.shape[1]),) 
```
#### 5.7 Reshape array with any shape to 1D 
```python
t16.flatten()
```

### 6. Calculation With Array

#### 6.1 Array vs. A number
- Add/suntract/mutiply/divide: operation is on each number in an array --> 广播机制

```python
# Example 1: 

t15 + 2
```
```python
# Example 2: 

t15/0

# output: [nan inf inf inf inf inf inf inf inf inf inf inf] --> nan == not a number; inf == infinity 
# numpy treat 0 as a very very small number, therefore 3/0 = "inf"
```
#### 6.2 Array vs. Array (same shape)
- calculation between arrays with exact same shape: 两个array中对应的数字进行运算

```python
t19 = np.arange(100, 124).reshape(4, 6)
t20 = np.arange(0,24).reshape(4, 6)
```
```python
t19 + t20
```
#### 6.3 Array vs. Array (partially different shape)
- calculation between arrays with partially different shape: 大array与小array的shape相同部分，与小array对应数字进行运算

```python
# Example 1: 

t21 = np.arange(0, 6)

t20 - t21

# t20的每一行与t21进行运算  
# t21 has a shape of (1, 6) --> 1 row, 6 columns
# t20 has a shape of (4, 6) --> 4 row, 6 columns
# output has a shape of (4, 6)
```
```python
# Example 2: 

t22 = np.arange(4).reshape((4, 1)) # t22 has a shape of (4, 1) -- 4 row, 1 columns 
    
print(t20 - t22)  

# t20的每一列与t22进行运算  
# t22 has a shape of (4, 1) --> 4 row, 1 columns 
# output has a shape of (4, 6)
```

#### 6.4 Array vs. Array (completely different shape)
- calculation between arrays with completely different shape: not capable 

#### 6.5 More Examples
1. Arrays (shapes) that are capable for calculation:
- (3, 3, 2) vs (1, 2)
- (3, 3, 2) vs (1, 3)
- (3, 3, 2) vs (3, 1)
- (3, 3, 2) vs (3, 2)
- (3, 3, 2) vs (3, 3)


2. Arrays (shapes) that are not capable for calculation: 
- (3, 3, 3) vs (3, 2)

