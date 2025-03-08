
# Pandas - Handling NaN

## Import Modules
```
import pandas as pd 
```

## Data Source
```
df1 = pd.DataFrame(np.arange(12).reshape(3, 4), index = list("abc"), columns = list("wxyz"))
df1["w"][1] = np.nan #[column][row]
```
```
df2 = pd.DataFrame(np.arange(12).reshape(3, 4), index = list("abc"), columns = list("wxyz"))
df2.iloc[1:, :2] = np.nan
```

## Handeling missing data (NaN)
- 0 可能是缺失值，可能是真实值 --> 需按实际情况判断

### 1. Detect Whether There is NaN
```
pd.isnull(df1) # 判断是NaN

pd.notnull(df1) # 判断不是NaN
```
### 2. Manipulate NaN 
#### 方法1: Delete NaN
```     
df_w = df1[pd.notnull(df1["w"])]  # 选中column w 中不是NaN的那一行

print(df_w)   # output:      w    x  y  z
                        a  0.0  1.0  2  3

df1.dropna(axis = 0) # delete all rows with nan

df1.dropna(axis = 0, how = "any")   # how = "any" --> this is the default setting --> delete all rows with nan

df1.dropna(axis = 1) # delete all columns with nan

df1.dropna(axis = 0, how = "all") # delete all rows that are all nan

df1.dropna(axis = 0, inplace = True) # inplace = True --> 对当前dataframe原地修改，不用在另存与一个新的dataframe中
```

#### 方法2: Refill data
```
df2.fillna(0,inplace = True) # replace NaN with 0 

df2.fillna(df2.mean(), inplace = True) # replace NaN with mean (column mean)

df2["w"].fillna(df2["w"].mean(), inplace = True) # operate only on column w and replace its NaN with column mean

df2["w"] = df2["w"].fillna(df2["w"].mean()) # althernative way to write the above commend

# df2["w"].mean() --> unlike numpy, the mean of a column with NaN is not NaN. 
                  --> Instead, it is the column mean of the sum of the rest of data point in the column 
```
- 注释：`df2["w"][1] = np.nan`的alternative: 
1. `df2["w"]["b"] = np.nan` --> 通用格式: [column][row]
2. `df2.loc["b", "w"] = np.nan`
3. `df2.iloc[1, 0] = np.nan`

### 3. 一些特殊处理的Tips
- 当不希望0参与到运算时，可将0变为NaN。例：`df2[df2 == 0] = np.nan`



