# Pandas - Join and Merge

## Import Modules
```python
import pandas as pd
import numpy as np
```
## Data Source
```python
df1 = pd.DataFrame(np.ones((2, 4)), index = ["A", "B"], columns = list("abcd"))
# print(df1)

df2 = pd.DataFrame(np.zeros((3, 3)), index = ["A", "B", "C"], columns = list("xyz")) 
# print(df2)

df3 = pd.DataFrame(np.zeros((3, 3)), columns = list("fax")) 
# print(df3)
```

## Functions
### 1. Join
- Join 时会出现的现象：
1. Index 或者 columns （index）相同会出现overlap报错
2. 两组df的index格式要一样：同为字母；同为数字
- Join特点：按照行索引（row index）

```python
df1.join(df2)

# output: -->  a    b    c    d    x    y    z
             # A  1.0  1.0  1.0  1.0  0.0  0.0  0.0
             # B  1.0  1.0  1.0  1.0  0.0  0.0  0.0
```
```python
df2.join(df1) 

# output: -->  x    y    z    a    b    c    d
             # A  0.0  0.0  0.0  1.0  1.0  1.0  1.0
             # B  0.0  0.0  0.0  1.0  1.0  1.0  1.0
             # C  0.0  0.0  0.0  NaN  NaN  NaN  NaN
```

### 2. Merge
- Merge特点： 按照列索引 （column index）
- 四种merge：
1. Merge默认：求两个df的交集 （inner） --> df1.merge(df3, on = "a", how = "inner")
2. Merge outer：求并集， NaN补全 --> df1.merge(df3, on = "a", how = "outer")
3. Merge left： 左边df为准，NaN补全 --> df1.merge(df3, on = "a", how = "left")
4. Merge right：右边df为准， NaN补全 --> df1.merge(df3, on = "a", how = "right")

```python
df1.merge(df3, on = "a") 

# on = "a"表示按照 column index “a“进行合并 
# output: empty dataframe 
```
```python
# Modify df3
df3 = pd.DataFrame(np.arange(9).reshape((3,3)), columns = list("fax")) 

df1.merge(df3, on = "a")

# output:      a    b    c    d  f  x
             # 0  1.0  1.0  1.0  1.0  0  2
             # 1  1.0  1.0  1.0  1.0  0  2
# df1中的a列为1时，其所在的row可以匹配到df3中a列为1时对应的row values。其他不对应的rows不会被打印
```
```python
# Modify df1
df1.loc["A", "a"] = 100

df1.merge(df3, on = "a")

df1.merge(df3, on = "a", how = "outer")

df1.merge(df3, on = "a", how = "left")

df1.merge(df3, on = "a", how = "right")

#当df中没有任何columns （index）相同时，用left_on 和 right_on来制定以哪两个column为merge标准:

df1.merge(df3, left_on = "b", right_on = "a", how = "right")
```
