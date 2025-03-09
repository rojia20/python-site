# Pandas - MultiIndex

## Import Modules
```python
import pandas as pd
import numpy as np
```
## Data Source
```python
df = pd.read_csv("data/starbucks.csv")

# 设置 pandas 打印选项，取消截断 --> 从而打印所有的列
pd.set_option("display.max_columns", None)

# check basic info about this dataset 
print(df.info())
print(df.head(10))
```

## What is MultiIndex
- Example:

```python
# Select column "Country" and "State/Province" from the original data file, and only keep the column "Brand"

group1 = df[["Brand"]].groupby(by = [df["Country"], df["State/Province"]]).count()

print(group1.index)
```


## Functions
### 1. 回顾Index
```python
# Step 1: create a dataframe

df1 = pd.DataFrame(np.ones((2, 4)), index = list("AB"), columns = list("abcd"))

df1.loc["A", "a"] = 100
```
```python
# 获取index：

df.index
```
### 2. 指定Index
```python
df.index = ['x','y']
```
### 3. 替换已有的index
```python
df1.index = ["a", "b"]

# 用a，b替换已有的index
```
### 4. 重新设置index 
```python
df.reindex(list("abcedf"))
```
```python
# 若原dataframe中没有“f“， f index对应的row，值都为NaN

df2 = df1.reindex(["a", "f"]) 
```
### 5. 指定某一列作为index
```python
# "Country"列（的values）作为索引(index)

df.set_index("Country",drop=False)
```
```python
# 将当前dataframe的a列（的values）作为索引（index）

df3 = df1.set_index("a") 
```
```python
df4 = df1.set_index("a", drop = False) 

# 默认：drop = True --> a列的值变成index， a列不见了
# drop = False --> a列的值变成index， 且保留a列
```
### 6. Create a DataFrame with MultiIndex
```python
# 指定某多列作为index --> 得到 mutiIndex

df5 = df1.set_index(["a", "b"])

df6 = df1.set_index(["a", "b", "c"])
```

### 7. Index 是可以重复的
```python
# 返回index的唯一值

df.set_index("Country").index.unique()
```
```python
df1.set_index("a").index.unique() 

# Index: [100.0, 1.0]
```
```python
df1.set_index("d").index.unique()

# Index: [1.0]
```

### 8. Length of Index
```python
len(df1.set_index("a").index)

# 相当于count the number of index 
```

### 9. Convert Index into a List 
```python
list(df1.set_index("a").index)
```

## Case One
```python
# create a dataframe 

a = pd.DataFrame({'a': range(7),'b': range(7, 0, -1),'c': ['one','one','one','two','two','two', 'two'],'d': list("hjklmno")})

b = a.set_index(["c", "d"])
```
```python
# select "one" and "j"

b.loc["one"].loc["j"] 
```
```python
# dataframe 中先取里层标签的做法

b.swaplevel().loc["h"]
```
- DataFrame中需要用loc 或者 iloc来取标签从而取值
- Series中可直接用标签名来取值 （例子如下）

```python
c = b["a"] 

# c is a series 
```
```python
c["one"]["j"]

# output: a data point
```
```python
# an alternative way for series 
c["one" , "j"]
```
```python
c["one"]

# output: a series
```
```python
d = a.set_index(["d", "c"])["a"]

# if we want to select "one"

# print(d.swaplevel())

d.swaplevel()["one"]
```

