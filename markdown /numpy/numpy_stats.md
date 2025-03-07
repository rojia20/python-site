# Numpy - 常见的统计方法

## Import Modules
```
import numpy as np
```

## 统计方法
- without asigning axis, opertaions will be on the entire array (all values in the array regardless its dimension)

### Sum
```
np.sum(t)
```
```
# an alternative way
t.sum 

# t is the name of an array
```
- #### Demo
```
# create an array
t1 = np.arange(24).reshape(4, 6)
t4 = t1.astype(float)
print(t4)
```
```
print(t4.sum(axis = 0))
```

### Mean
```
print(t4.mean(axis = 0))
```

### Median
```
print(np.median(t4, axis = 0))
```

### Max
```
print(t4.max(axis = 0))
```

### Min
```
print(t4.min(axis = 0))
```

### Range: Max - Min
```
print(np.ptp(t4, axis = 0))

# ptp: peak-to-peak
```

### Standard Deviation
- Describe the distribution/dispersion of sample mean
```
print(t4.std(axis = 0))
```


