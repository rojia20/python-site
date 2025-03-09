# Numpy - Other Functions

## Import Modules
```python
import numpy as np
import random
```

## Data Source
```python
t1 = np.arange(15).reshape(3, 5)
```

## Functions
### 1. Identify the location of the max and min of an array
- ```np.argmax()```
- ```np.argmin()```

```python
np.argmax(t1, axis = 0) 

# axis = 0 meaning: the output is same shape as a row --> find the colum max or min 
# output: [2 2 2 2 2] --> 2 meaning the column max is at second row
```
```python
np.argmin(t1, axis = 1) 

# axis = 1 meaning: the output is same shape as a column --> find the row max or min 
# output: [0 0 0] --> 0 meaning the row min is at the first column
```

### 2. Replace multiple data points of same value in an array by a different value
```python
t2 = np.eye(5)   

# Replace ones by -1 for t2 array:

t2[t2 == 1] = -1 
```
```python
np.argmin(t2, axis = 0)  

# the column min is at [0 1 2 3 4]           
```

### 3. Create an array: with all zeros
```python
np.zeros((3, 4))
```

### 4. Create an array: with all onces
```python
np.ones((3, 4))
```

### 5. Create an array: shape of square and the diagonal are ones
- the "top-left-to-bottom-right" diagonal are ones

```python
np.eye(3) 

# 括号中的3表示：3 by 3 matrix
```
### 6. Create an array: with random float numbers (0~1)
- Random float numbers (0~1) are evenly distributed 
- ```np.random.rand(size)```

```python
np.random.rand(1, 2)
```

### 7. Create an array: with random float numbers (negative or positive)
- Random float numbers (negative or positive) are normally distributed 
- standardized with mean = 0 and SD = 1
- ```np.random.randn(size)```

```python
np.random.randn(1, 2)
```

### 8. Create an array: with random numbers, defining the lowest and highest number and shape
- ```np.random.randint(low, high, (shape))```

```python
np.random.randint(10, 20, (4, 5))

# 4行5列的array中是10～20间的随机正数
```

### 9. Create an array: with evenly distributed random float numbers, defining the lowest and highest number and size
- size is shape
- ```np.random.uniform(low, high, (size))```

```python
np.random.uniform(10, 20, (4,5))
```

### 10. Randomly select from the normal distributed sample, specifing the center = loc, SD = scale, and shape = size
- ```np.random.normal(loc, scale, (size))```

### 11. Set a seed so that each time generating the extact same random array （前提是在同一台电脑上）
- ```np.random.seed(s)```

```python
np.random.seed(10)

t = np.random.randint(0, 20, (3,4))
```

### 12. View
- ```a = b``` --> a和b完全不复制，a和b相互影响, b的值都进入a
- ```a = b[:]``` --> 视图操作，a和b相互影响 --> if a change, b will change accordingly 

### 13. Copy 
- ```a = b.copy()``` --> a和b互不影响
- Best practice: ```b = b```， 避免以上情况
