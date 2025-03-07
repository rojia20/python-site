# Numpy - Handling Missing Data (NaN)

## Import Modules
```
import numpy as np
```
## Data Source
```
t1 = np.arange(12).reshape(3, 4).astype(float)
t1[1, 2:] = np.nan 
```

## Case One: calculating the average 
- Without asigning axis, opertaions will be on the entire array (all values in the array regardless its dimension)
```
Define a function that calculate column mean:

def fill_ndarray(t1): # define a function that calculate column mean
    for i in range (t1.shape[1]): # read through each column
        temp_col = t1[:, i] # select the current column
        nan_num = np.count_nonzero(np.isnan(temp_col))
        if nan_num != 0: # there is nan
            temp_nonan_col = temp_col[temp_col == temp_col] # select parts of the current column that are nan free --> form a new array without nan (next step: find its mean)
            temp_col[temp_col != temp_col] = temp_nonan_col.mean() # replace the current nan with the average 
    return t1
```
```
Call out the self-defined function to fill the NaN with column mean: 

if __name__ == '__main__': # only run following code in this local file, not when importing self-define function in other file
    t1 = np.arange(12).reshape(3, 4).astype(float)
    t1[1, 2:] = np.nan 
    print(t1)   # output: [[ 0.  1.  2.  3.],[ 4.  5. nan nan],[ 8.  9. 10. 11.]]
    t1 = fill_ndarray(t1)
    print(t1)   # output: [[ 0.  1.  2.  3.],[ 4.  5.  6.  7.],[ 8.  9. 10. 11.]]
                # 6 is the mean of (2 + 10), and 7 is the mean of (3 + 11)
```