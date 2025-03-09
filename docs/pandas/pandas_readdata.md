# Pandas - Read Data

## 前言
- Pandas中大小写matters

## Import Modules
```python
import pandas as pd 
import numpy as np
import string
```

## Data Source
- Read CSV file

```python
df = pd.read_csv("/Users/jrq/Desktop/learnpy/data/dognames.csv")

# check data 
print(df.head(), df.info())
```


## Functions
### 1. Sort/Rank 
- Practice question: which dog name is the most frequently used?

```python
# rank the names based of the name counts 
df_sort = df.sort_values(by = "Count_AnimalName", ascending = False) # ascending: default is True
```

### 2 Select Rows and/or Columns
#### 2.1 Select Top Rows
```python
# select the top 5

print(df_sort.head(5))
```
#### 2.2 Select Rows/Columns Using Slice
```python
# 1. select the first 100 rows：

df_sort[:100]

# []中直接写数字表示按row操作
```
```python
# 2. select by columns 

df_sort["Row_Labels"]

# []中写“字符串“表示按column操作 -- output is a series
```
```python
# 3. select by columns and rows 

df_sort[:20]["Row_Labels"]

# [row][column] --> 先取前20行，再取row_labels这一列
```
```python
# 4. select certain rows and columns 

df1 = pd.DataFrame(np.arange(12).reshape(3, 4), index = list("abc"), columns = list("wxyz"))
df1["w"][1] = np.nan #[column][row]
df1["w"]["b"] = np.nan # alternative way
```

- 为什么 #4 切片是先列后行，而 #3 是先行后列：
1. DataFrame 的默认索引方式是列优先（`df[column]`），而不是行优先。因为列操作（如选择、计算）更常见。
   - `df2["w"][1]` 只能先列后行，因为 `df2["w"]` 返回的是 Series，而 Series 是一个一维数据结构，只有索引（行）没有列
2. `df_sort[:20]["Row_Labels"]` 可以先行后列，因为 `df_sort[:20]` 返回的是 DataFrame，既有行索引也有列索引。
    - `["Row_Labels"]` 从这个新的 DataFrame 中选择列 "Row_Labels"，返回一个 Series。

#### 2.3 Best Practice: Select Rows/Columns Based on Index
```python
df1.loc["a","z"]

# ["row index","column index"] --> 表示a行，z列
```
```python
df1.loc["a"]

# select only row a and all columns
```
```python
df1.loc["a",:]
# select only row a and all columns
```
```python
df1.loc[:,"z"]

# select only column z
```
```python
df1.loc[["a","c"],"z"]

# select only row a and c, and column z
```
```python
df1.loc[["a","c"], ["z", "w"]]

# select only row a and c, and column z and w
```
```python
df1.loc["a":"c", ["z", "w"]]

# select only row a to c (inclusively), and column z and w only
# 与普通切片不同，这里的row c是被包含选中的
```

#### 2.4 Best Practice: Select Rows/Columns Based on location
```python
df1.iloc[1]

# select the second row 
```
```python
df1.iloc[:, 2]

# select all rows but only the third column
```
```python
df1.iloc[:, [2, 1]]

# select all rows but only the second and third column 
```
```python
df1.iloc[[0,2], [2, 1]]

# select the first and third row and the second and third column 
```
```python
df1.iloc[1:, :2]

# select all rows since the second row, and select all columns before the third column
```
### 3 Assign values to row/column/a data point
```python
df1.iloc[1:, :2] = 30
```

### 4. Assign NaN to row/column/a data point
```python
df1.iloc[1:, :2] = np.nan 

# 不同于numpy，pandas会将数据自动转换成float type，然后再assign NaN

# alternatives: 

df1.loc["b", "w"] = np.nan  
```

### 5. 布尔索引
```python
df_sort[df_sort["Count_AnimalName"] > 800]
```

- When having multiple conditions:                              
    1. & --> 表示“且”，for having more than one condition concurrently              
    2. | --> 表示“或”，meeting one condition or the other               

```python
# Have more than one condition concurrently:

df_sort[(800 < df_sort["Count_AnimalName"]) & (df_sort["Count_AnimalName"] < 1000)]
```
```python
df_sort[(df_sort["Row_Labels"].str.len() > 4) & (df_sort["Count_AnimalName"] > 700)]
```
```python
# Meet one condition or the other 

df_sort[(800 < df_sort["Count_AnimalName"]) | (df_sort["Count_AnimalName"] < 1000)]
```

### 6. str的多种方法
```str.cat()``` --> 用于字符串链接，可指定分隔符        
`str.contains()`--> 字符串包含指定模式的布尔数组        
`str.count()`   
`str.endswith()`    
```str.startswith()```  
`str.findall()`     
`str.get()`     
`str.join()`        
`str.len()` --> 用于区字符串的长度      
`str.lower()` 小写      
`str.upper()` 大写      
`str.match()`       
`str.pad()`     
`str.center()`      
`str.repeat()` --> 对各个字符串执行三次     
`str.replace()`     
`str.slice()`       
`str.split()`       
`str.strip().tolist()` --> 字符串除去空白、换行 --> 得列表      
`str.rstrip()`      
`str.lstrip()`      



