# Numpy - 常见的统计方法

## Import Modules
```python
import numpy as np
```

## Statistical Functions
- Without asigning axis, opertaions will be on the entire array (all values in the array regardless its dimension)

### 1. Sum
```python
方法1；

np.sum(t)
```
```python
方法2:

t.sum 

# t is an array
```
#### Demo
```python
# Create an array：

t1 = np.arange(24).reshape(4, 6)
t4 = t1.astype(float)
```
```python
# 求每一列的和 (column total):

t4.sum(axis = 0)
```

### 2. Mean
```python
t4.mean(axis = 0)
```

### 3. Median
```python
np.median(t4, axis = 0)
```

### 4. Max
```python
t4.max(axis = 0)
```

### 5. Min
```python
t4.min(axis = 0)
```

### 6. Range: Max - Min
```python
np.ptp(t4, axis = 0)

# ptp: peak-to-peak
```

### 7. Standard Deviation
- Describe the distribution/dispersion of sample mean

```python
t4.std(axis = 0)
```


