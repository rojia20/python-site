# Numpy - 读取数据

## 前言
- 读取数据一般不用numpy，而是pandas
    - pandas更强大
- Data file的格式通常是CSV file (comma-separated value)
    - np.loadtxt(fname,dtype=np.float,delimiter=None,skiprows=0,usecols=None,unpack=False)
        - delimiter --> 分隔字符串；默认是空格，可改为逗号
        - skiprows --> 跳过前X行
        - usecols --> 读取指定的列
        - unpack --> 转制: 将行转成列，将列转成行 
            - 默认为 unpack = False

## Import Modules
```
import numpy as np
```

## Read CSV file 
```
us_file_path = "./data/us_videos.csv"

uk_file_path = "./data/gb_videos.csv"
```
```
us = np.loadtxt(us_file_path, delimiter = ",", dtype = "int", skiprows = 1)

uk = np.loadtxt(uk_file_path, delimiter = ",", dtype = "int", skiprows = 1)
```

## 转置的方法
```
t1 = np.arange(24).reshape(4, 6)
print(t1)
```
### Demo 1
```
print(t1.transpose())
```
### Demo 2:
```
print(t1.T)
```

## Extract certain row(s) or column(s)
- using []
- 基本格式：us[rows, columns]

### Extract one row
```
# extract the third row 
print(us[2]) 
```
```
# an alternative way
print(us[2, :]) 
```

### Extract mutiple rows 
```
# extract second and thrid rows 
print(us[1:3]) 
```
```
# extract every row after the thrid row
print(us[2:]) 
```
```
# extract multiple but inconsistant rows
print(us[[2, 8, 10]]) 
```

### Extract one column
```
# extract the thrid column
# : 表示对rows不做特别处理
print(us[:, 2]) 
```

### Extract multiple columns
```
# extracting the second and third columns 
print(us[:, 1:3]) 
```
```
# extract every column after the thrid column
print(us[:, 2:])
```
```
# extract multiple but inconsistant columns
print(us[:, [0, 1, 3]]) 
```

### Extract one row and one column 
- This is equivalent to extracting a data point

```
a = us[2, 3] 
print(a)
```
```
# check the data type of a
print(type(a)) 

# output: data type = numpy.int64
```

### Extract multiple rows and multiple columns (continuous)
```
b = us[2:5, 1:4]
print(b)
```

### Extract multiple rows and multiple columns (inconsistant) 
- This is equivalent to extracting mutiple data points

```
# 取matrix（数阵）中不相邻的两个点 --> 点坐标, 例：一行一列（0， 0），三行二列 （2， 1））
c = us[[0, 2], [0, 1]] 
print(c)
```

## 取步长
- 例：using [:2]

```
# 每两列一取 --> ：2 表示 step == 2 
print(us[:, 2::2]) 
```
```
# star from the second column, and step is 2, including the fourth column 
print(us[:, 1::2]) 
```

## Manipulating Data

### Manipulate data points all at once

- #### Original data
```
print(us[1,1:4]) 
```

- #### Assign 0 to all
```
us[1,1:4] = 0 
print(us[1,1:4])
```

### Manipulate data points with conditions
- #### Manipulate data points that are less than or equal to 10 
```
t1[t1 <= 10] = 3
print(t1)  
```
 - *原理:*  
    - *t1 < 10 gives an output that has a dtype = bool （True or False）*
    - *t1[t1 <= 10] = 3 --> 将 t1 matrix 中 True 的位置统统替换为3*

- #### Replace t1 < 10 with 0 and t1 > 10 with 10 
    - 一个临界点
```
t2 = np.where(t1 < 10, 0, 10)
print(t2)
```
- *解析:*
    - *if t1 < 10, then t1 = 0, otherwise t1 = 10*

- #### Replace t1 < 10 with 10 and t1 > 18 with 18 
    - 两个临界点
```
# clip 用来裁剪
t3 = t1.clip(10, 18)
print(t3)
```

- #### 赋值 a data with NaN 
    - data must be float before converting
```
t4 = t1.astype(float)
t4[3, 3] = np.nan 
print(t4)
```

## Footnotes
Using a divider when coding can achieve better visualization and clarity 

- Example:
```
print("*"*100)
````
