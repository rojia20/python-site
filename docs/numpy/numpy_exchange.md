# Numpy - Exchange Rows or Columns

## Import Modules
```
import numpy as np
import random
```

## Data Source
```
Create an array:

t = np.arange(12, 24).reshape(3, 4)
```
Output: 
[[12 13 14 15]
 [16 17 18 19]
 [20 21 22 23]]

## Functions

### Example 1: exchange the second and third row 
```
t[[1, 2], :] = t[[2, 1], :] 

# keep the columns intact

print(t)
```
```
Output: 
[[12 13 14 15]
 [20 21 22 23]
 [16 17 18 19]]
```

### Example 2: exchange the first and second row 
```
t[:, [0, 2]] = t[:, [2, 0]] 

# keep the rows intact

print(t)
```
```
Output: 
[[14 13 12 15]
 [22 21 20 23]
 [18 17 16 19]]
```