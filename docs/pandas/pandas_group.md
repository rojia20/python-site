# Pandas - Group and 聚合Functions

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
```
```python
# Check basic info about this dataset 

print(df.info())
print(df.head(10))
```

## Functions
### 1. Group
```python
# Step 1: group the data by country 

country_group = df.groupby(by = "Country")

# print(country_group ) # output: DataFrameGroupBy --> 可用于遍历&调用聚合方法
```
```python
# Step 2: 遍历country_group (元组: 索引（=分组的值) + 分组后的dataframe）
for i, j in country_group: 
    print(i)
    print("-"*100)
    print(j, type(j)) # j is dataframe
```
```python
# Step 3: eg.只读取英国数据

df[df["Country"] == "US"]
```
```python
# Step 4: 调用聚合方法 --> 统计每个国家的每列的个数

country_group.count()

# 只统计特定column:
country_group["Brand"].count()
```

### 2. 聚合的Functions
- `count()`   
- `sum()`   
- `mean()`    
- `median()`    
- `std()`    
- `var()`    
- `min()`    
- `max()`    

## Case One: 
### Background: 
- 现有关于全球星巴克的信息

### Question
- 美国的星巴克数量和中国的比较，谁更多？

### Solution 
```python
star_by_country = country_group["Brand"].count()

us_star = star_by_country["US"]


cn_star = star_by_country["CN"]

# Based on comparison, US has more Starbucks
```

### Case Two
### Background: 
- 沿用全球星巴克的信息

### Question
- 中国每个省的星巴克数量的情况是怎样的

### Solution
```python
# Step 1: only take out data about China

star_china = df[df["Country"] == "CN"]
```
```python
# Step 2: group the China data by province and count the number of Starbucks (brand) in each province

star_cn_state = star_china.groupby(by = "State/Province").count()["Brand"]
```

### Case Three
### Background: 
- 沿用全球星巴克的信息

### Question 
- 对国家和省/州同时进行分组

### Solution 
```python
grouped = df.groupby(by = ["Country", "State/Province"])
```
```python
# 获取分组后的某一部分数据（列）
df.groupby(by = ["Country", "State/Province"])["Country"].count()
```
```python
# 获取分组后的某一部分数据 (行）
star_count = df["Brand"].groupby(by = [df["Country"], df["State/Province"]]).count()

# 因为df["Brand"]中本身没有”Country“和”State/Province“这两列，所以一定要先规定df[]

print(star_count) # output is a series with two indexs (country and province)
```
```python
#if we want the output is a dataframe instead: 

group1 = df[["Brand"]].groupby(by = [df["Country"], df["State/Province"]]).count()
group2 = df.groupby(by = ["Country", "State/Province"])[["Brand"]].count()
group3 = df.groupby(by = ["Country", "State/Province"]).count()[["Brand"]]

# ["Brand"] --> []用于强调取某一列和多列。这里特别指出只取“Brand”这一列， 所以返回的是dataframe
```
