# Numpy - 常见的统计方法

## Import Modules
```
import numpy as np
```

## Statistical Functions
- without asigning axis, opertaions will be on the entire array (all values in the array regardless its dimension)

### 1. Sum
```
方法1；

np.sum(t)
```
```
方法2:

t.sum 

# t is an array
```
#### Demo
```
create an array：

t1 = np.arange(24).reshape(4, 6)
t4 = t1.astype(float)
```
```
求每一列的和 (column total):

t4.sum(axis = 0)
```

### 2. Mean
```
t4.mean(axis = 0)
```

### 3. Median
```
np.median(t4, axis = 0)
```

### 4. Max
```
t4.max(axis = 0)
```

### 5. Min
```
t4.min(axis = 0)
```

### 6. Range: Max - Min
```
np.ptp(t4, axis = 0)

# ptp: peak-to-peak
```

### 7. Standard Deviation
- Describe the distribution/dispersion of sample mean
```
t4.std(axis = 0)
```


