### Chapter 3：用序列表示單變數資料

### 3.1 設定pandas==>pd.set_option

```
# import numpy and pandas
import numpy as np
import pandas as pd

# used for dates
import datetime
from datetime import datetime, date

# Set some pandas options controlling output format
pd.set_option('display.notebook_repr_html', False)
pd.set_option('display.max_columns', 8)
pd.set_option('display.max_rows', 10)
pd.set_option('display.width', 80)

# bring in matplotlib for graphics
import matplotlib.pyplot as plt
%matplotlib inline

https://www.yiibai.com/pandas/python_pandas_options_and_customization.html
Pandas提供API來自定義其行為的某些方面，大多使用來顯示。

API由五個相關函數組成。它們分別是-
1.get_option()
2.set_option()
3.reset_option()
4.describe_option()
5.option_context()

1.get_option(param)需要一個參數，並返回下面的輸出中給出的值-

#import pandas as pd
print ("display.max_rows = ", pd.get_option("display.max_rows"))

結果- 
display.max_rows =  60

2.set_option(param,value)需要兩個參數，可以更改要顯示的預設行數。

#import pandas as pd

#print ("before set display.max_rows = ", pd.get_option("display.max_rows")) 

#pd.set_option("display.max_rows",80)
print ("after set display.max_rows = ", pd.get_option("display.max_rows"))

結果- 
before set display.max_rows =  60
after set display.max_rows =  80

3.reset_option(param)-接受一個參數，成為該值設置為替換值。

#import pandas as pd

#pd.set_option("display.max_rows",32)
print ("after set display.max_rows = ", pd.get_option("display.max_rows")) 

#pd.reset_option("display.max_rows")
print ("reset display.max_rows = ", pd.get_option("display.max_rows"))

結果- 
after set display.max_rows =  32
reset display.max_rows =  60

4.describe_option(param)-打印參數的描述

#import pandas as pd
pd.describe_option("display.max_rows")

結果- 
display.max_rows : int
    If max_rows is exceeded, switch to truncate view. Depending on
    `large_repr`, objects are either centrally truncated or printed as
    a summary view. 'None' value means unlimited.

    In case python/IPython is running in a terminal and `large_repr`
    equals 'truncate' this can be set to 0 and pandas will auto-detect
    the height of the terminal and print a truncated object which fits
    the screen height. The IPython notebook, IPython qtconsole, or
    IDLE do not run in a terminal and hence it is not possible to do
    correct auto-detection.
    [default: 60] [currently: 60]
    
5.option_context()當退出使用塊時，選項值將自動恢復-
#import pandas as pd
with pd.option_context("display.max_rows",10):
   print(pd.get_option("display.max_rows"))
   print(pd.get_option("display.max_rows"))
   
結果- 
10
10

```

### 屬性值DateTime

```
新的物件，具有與這個執行個體相同的日期，並將時間值設定為午夜 12:00:00 (00:00:00)。

範例
下列範例會使用 Date 屬性來解壓縮 DateTime 值的日期元件，並將其時間元件設定為零（或0:00:00 或午夜）。 
它也會說明，根據顯示 DateTime 值時所使用的格式字串，時間元件可以繼續出現在格式化輸出中。

備註
傳回之 DateTime 值的 Kind 屬性值，與目前實例的值相同。
因為 DateTime 類型代表單一類型中的日期和時間，所以請務必避免將 Date 屬性傳回的日期錯誤解譯為日期和時間。

#using System;

public class Example
{
   public static void Main()
   {
      DateTime date1 = new DateTime(2008, 6, 1, 7, 47, 0);
      Console.WriteLine(date1.ToString());
      
      // Get date-only portion of date, without its time.
      DateTime dateOnly = date1.Date;
      // Display date using short date string.
      Console.WriteLine(dateOnly.ToString("d"));
      // Display date using 24-hour clock.
      Console.WriteLine(dateOnly.ToString("g"));
      Console.WriteLine(dateOnly.ToString("MM/dd/yyyy HH:mm"));   
   }
}
// The example displays output like the following output:
//       6/1/2008 7:47:00 AM
//       6/1/2008
//       6/1/2008 12:00 AM
//       06/01/2008 00:00
```

### 資料視覺化(Matplotlib, Seaborn, Plotly)

```
資料視覺化除了最後一步呈現你的成果之外，還可以在分析的過程中用資料視覺化來看出一些insight，
比方說用熱點圖來看你的Deep learning的model是對圖片中哪一部分的看得較重要，
或是可以降維之後將資料視覺化去看資料在空間中的分佈，來決定下一步的分析要怎麼做。

Python資料視覺化主要有三大套件：
Matplotlib

Seaborn

Plotly

```

### 3.2 建立序列==>pd.Series()

```
Pandas是一個基於Numpy的package，在處理數據方面非常的好用簡單，
在學習pandas之前我們要先知道pandas的兩種特有的資料結構DataFrame與Series。
```
### 資料類型 - Series
```
Series，是一個類似陣列的物件，裡面可包含陣列的資料。
```
### 資料類型 - DataFrame
```
DataFrame就像是我們在使用的excel表格一樣，是一個二維的數據有index和column，
可以透過index和column來找到我們要的某一筆資料。

区别：
      series，只是一个一维数据结构，它由index和value组成。
      dataframe，是一个二维结构，除了拥有index和value之外，还拥有column。
联系：
      dataframe由多个series组成，无论是行还是列，单独拆分出来都是一个series。
```
### 3.2.1使用Python串列和字典來建立序列
```
# create a series of multiple values from a list
s = pd.Series([10, 11, 12, 13, 14])
s

結果:
0    10
1    11
2    12
3    13
4    14
dtype: int64

# value stored at index label 3
s[3]

結果:
13

# create a Series of alphas
pd.Series(['Mike', 'Marcia', 'Mikael', 'Bleu'])

結果:
0      Mike
1    Marcia
2    Mikael
3      Bleu
dtype: object

# a sequence of 5 values, all 2
pd.Series([2]*5)

結果:
0    2
1    2
2    2
3    2
4    2
dtype: int64

# use each character as a value
pd.Series(list('abcde'))


結果:
0    a
1    b
2    c
3    d
4    e
dtype: object

# create Series from dict
pd.Series({'Mike': 'Dad', 
           'Marcia': 'Mom', 
           'Mikael': 'Son', 
           'Bleu': 'Best doggie ever' })
           
結果:
Bleu      Best doggie ever
Marcia                 Mom
Mikael                 Son
Mike                   Dad
dtype: object
```

```
pandas.Series
class pandas.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)

```
Parameters

data:array-like, Iterable, dict, or scalar value
Contains data stored in Series.
Changed in version 0.23.0: If data is a dict, argument order is maintained for Python 3.6 and later.

index:array-like or Index (1d)
Values must be hashable and have the same length as data. Non-unique index values are allowed. Will default to RangeIndex (0, 1, 2, …, n) if not provided. If both a dict and index sequence are used, the index will override the keys found in the dict.

dtype:str, numpy.dtype, or ExtensionDtype, optional
Data type for the output Series. If not specified, this will be inferred from data. See the user guide for more usages.

name:str, optional
The name to give to the Series.

copy:bool, default False
Copy input data.
```

https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html

```

### 3.2.2使用NumPy函數創建序列
```
# 4 through 8
pd.Series(np.arange(4, 9))

結果:
0    4
1    5
2    6
3    7
4    8
dtype: int64
```
### arange()函数
```
函數說明：arange([start,] stop[, step,], dtype=None)根據start與stop指定的範圍以及step設定的步長，生成一個 ndarray。
dtype : dtype The type of the output array.  
If `dtype` is not given, infer the data type from the other input arguments.
```
```
# 0 through 9
pd.Series(np.linspace(0, 9, 5))

結果:
0    0.00
1    2.25
2    4.50
3    6.75
4    9.00
dtype: float64
```
### numpy中linspace用法
```
linspace的功能最初是從MATLAB中學來的，用此來創建等差數列。近期用Python的時候發現也有這個功能，提供相應功能的是numpy。
```
```
# random numbers
np.random.seed(12345) # always generate the same values
# 5 normally random numbers
pd.Series(np.random.normal(size=5))

結果:
0   -0.204708
1    0.478943
2   -0.519439
3   -0.555730
4    1.965781
dtype: float64
```
### 3.2.3 使用純量值建立序列
```
# create a one item Series
s = pd.Series(2)
s

結果:
0    2
dtype: int64

# create the Series
s = pd.Series(np.arange(0, 5))
# multiple all values by 2
s * 2

結果:
0    0
1    2
2    4
3    6
4    8
dtype: int64
```

### 3.3 .index及.values屬性
### Python 字典(Dictionary) values()方法
```
描述
Python 字典(Dictionary) values() 函数以列表返回字典中的所有值。

语法
dict.values()

参数
NA。
```
```
# what is one day from 2014-11-30?
today = datetime(2014, 11, 30)
tomorrow = today + pd.Timedelta(days=1)
tomorrow

結果:
datetime.datetime(2014, 12, 1, 0, 0)
```
### timedelta 类对象
```
timedelta 对象表示两个 date 或者 time 的时间间隔。

class datetime.timedelta(days=0, seconds=0, microseconds=0, milliseconds=0, minutes=0, hours=0, weeks=0)
所有参数都是可选的并且默认为 0。 这些参数可以是整数或者浮点数，也可以是正数或者负数。

只有 days, seconds 和 microseconds 会存储在内部。 参数单位的换算规则如下：

1毫秒会转换成1000微秒。

1分钟会转换成60秒。

1小时会转换成3600秒。

1星期会转换成7天。

并且 days, seconds, microseconds 会经标准化处理以保证表达方式的唯一性，即：

0 <= microseconds < 1000000

0 <= seconds < 3600*24 (一天的秒数)

-999999999 <= days <= 999999999
```

```
# show that this is a numpy array
type(s.values)

結果:
numpy.ndarray

# get the index of the Series
s.index

結果:
RangeIndex(start=0, stop=3, step=1)


```

### 3.4 序列的大小及形狀
```
# example series
s = pd.Series([0, 1, 2, 3])
len(s)

結果:
4

# .size is also the # of items in the Series
s.size

結果:
4

# .shape is a tuple with one value
s.shape

結果:
(4,)

```

### 3.5 在序列建立時指定索引
```
# explicitly create an index
labels = ['Mike', 'Marcia', 'Mikael', 'Bleu']
role = ['Dad', 'Mom', 'Son', 'Dog']
s = pd.Series(labels, index=role)
s

結果:
Dad      Mike
Mom    Marcia
Son    Mikael
Dog      Bleu
dtype: object

# examine the index
s.index

結果:
Index(['Dad', 'Mom', 'Son', 'Dog'], dtype='object')

# who is the Dad?
s['Dad']

結果:
'Mike'
```

### 3.6 頭、尾、選取
```
# a ten item Series
s = pd.Series(np.arange(1, 10), 
              index=list('abcdefghi'))


# show the first five
s.head()

結果:
a    1
b    2
c    3
d    4
e    5
dtype: int64

# the first three
s.head(n = 3) # s.head(3) is equivalent

結果:
a    1
b    2
c    3
dtype: int64

# the last five
s.tail()

結果:
e    5
f    6
g    7
h    8
i    9
dtype: int64

# the last 3
s.tail(n = 3) # equivalent to s.tail(3)

結果:
g    7
h    8
i    9
dtype: int64

# only take specific items by position
s.take([1, 5, 8])

結果:
b    2
f    6
i    9
dtype: int64
```

### 3.7 以索引標籤或位置提取序列值
### 3.7.1利用[]運算子及ix[]屬性以標籤查詢
```
# we will use this series to examine lookups
s1 = pd.Series(np.arange(10, 15), index=list('abcde'))
s1

結果:
a    10
b    11
c    12
d    13
e    14
dtype: int64

# get the value with label 'a'
s1['a']

結果:
10

# get multiple items
s1[['d', 'b']]

結果:
d    13
b    11
dtype: int64

# gets values based upon position
s1[[3, 1]]

結果:
d    13
b    11
dtype: int64

# to demo lookup by matching labels as integer values
s2 = pd.Series([1, 2, 3, 4], index=[10, 11, 12, 13])
s2

結果:
10    1
11    2
12    3
13    4
dtype: int64

# this is by label not position
s2[[13, 10]]

結果:
13    4
10    1
dtype: int64
```

### 3.7.2以.iloc[]指明位置查詢
```
# explicitly  by position
s1.iloc[[0, 2]]

結果:
a    10
c    12
dtype: int64

# explicitly  by position
s2.iloc[[3, 2]]

結果:
13    4
12    3
dtype: int64
```
### 3.7.3以.loc[]指明標籤查詢
```
# explicit via labels
s1.loc[['a', 'd']]

結果:
a    10
d    13
dtype: int64

# get items at position 11 an d12
s2.loc[[11, 12]]

結果:
11    2
12    3
dtype: int64

# -1 and 15 will be NaN
s1.loc[['a', 'f']]

結果:
a    10.0
f     NaN
dtype: float64
```

### 3.8 把序列切割成子集合
```
# a Series to use for slicing
# using index labels not starting at 0 to demonstrate 
# position based slicing
s = pd.Series(np.arange(100, 110), index=np.arange(10, 20))
s

結果:
10    100
11    101
12    102
13    103
14    104
15    105
16    106
17    107
18    108
19    109
dtype: int64

# slice showing items at position 1 thorugh 5
s[1:6]

結果:
11    101
12    102
13    103
14    104
15    105
dtype: int64

# lookup via list of positions
s.iloc[[1, 2, 3, 4, 5]]

結果:
11    101
12    102
13    103
14    104
15    105
dtype: int64

# items at position 1, 3, 5
s[1:6:2]

結果:
11    101
13    103
15    105
dtype: int64

# first five by slicing, same as .head(5)
s[:5]

結果:
10    100
11    101
12    102
13    103
14    104
dtype: int64

# fourth position to the end
s[4:]

結果:
14    104
15    105
16    106
17    107
18    108
19    109
dtype: int64

# every other item in the first five positions
s[:5:2]

結果:
10    100
12    102
14    104
dtype: int64

# every other item starting at the fourth position
s[4::2]

結果:
14    104
16    106
18    108
dtype: int64

# reverse the Series
s[::-1]

結果:
19    109
18    108
17    107
16    106
15    105
14    104
13    103
12    102
11    101
10    100
dtype: int64

# every other starting at position 4, in reverse
s[4::-2]

結果:
14    104
12    102
10    100
dtype: int64

# -4:, which means the last 4 rows
s[-4:]

結果:
16    106
17    107
18    108
19    109
dtype: int64

# :-4, all but the last 4
s[:-4]

結果:
10    100
11    101
12    102
13    103
14    104
15    105
dtype: int64

# equivalent to s.tail(4).head(3)
s[-4:-1]

結果:
16    106
17    107
18    108
dtype: int64

# used to demonstrate the next two slices
s = pd.Series(np.arange(0, 5), 
              index=['a', 'b', 'c', 'd', 'e'])
s

結果:
a    0
b    1
c    2
d    3
e    4
dtype: int64

# slices by position as the index is characters
s[1:3]

結果:
b    1
c    2
dtype: int64

# this slices by the strings in the index
s['b':'d']

結果:
b    1
c    2
d    3
dtype: int64
```
### 3.9 利用索引標籤實現對齊
```
# First series for alignment
s1 = pd.Series([1, 2], index=['a', 'b'])
s1

結果:
a    1
b    2
dtype: int64

# Second series for alignment
s2 = pd.Series([4, 3], index=['b', 'a'])
s2

結果:
b    4
a    3
dtype: int64

# add them
s1 + s2

結果:
a    4
b    6
dtype: int64

# multiply all values in s3 by 2
s1 * 2

結果:
a    2
b    4
dtype: int64

# scalar series using s3's index
t = pd.Series(2, s1.index)
t

結果:
a    2
b    2
dtype: int64

# multiply s1 by t
s1 * t

結果:
a    2
b    4
dtype: int64

# we will add this to s1
s3 = pd.Series([5, 6], index=['b', 'c'])
s3

結果:
b    5
c    6
dtype: int64

# s1 and s3 have different sets of index labels
# NaN will result for a and c
s1 + s3

結果:
a    NaN
b    7.0
c    NaN
dtype: float64

# 2 'a' labels
s1 = pd.Series([1.0, 2.0, 3.0], index=['a', 'a', 'b'])
s1

結果:
a    1.0
a    2.0
b    3.0
dtype: float64

# 3 a labels
s2 = pd.Series([4.0, 5.0, 6.0, 7.0], index=['a', 'a', 'c', 'a'])
s2

結果:
a    4.0
a    5.0
c    6.0
a    7.0
dtype: float64

# will result in 6 'a' index labels, and NaN for b and c
s1 + s2

結果:
a    5.0
a    6.0
a    8.0
a    6.0
a    7.0
a    9.0
b    NaN
c    NaN
dtype: float64
```

### 3.10 執行布林選擇
```
# which rows have values that are > 5?
s = pd.Series(np.arange(0, 5), index=list('abcde'))
logical_results = s >= 3
logical_results

結果:
a    False
b    False
c    False
d     True
e     True
dtype: bool

# select where True
s[logical_results]

結果:
d    3
e    4
dtype: int64

# a little shorter version
s[s > 5]

結果:
Series([], dtype: int64)

# commented as it throws an exception
# s[s >= 2 and s < 5]

# correct syntax
s[(s >=2) & (s < 5)]

結果:
c    2
d    3
e    4
dtype: int64

# are all items >= 0?
(s >= 0).all()

結果:
True

# any items < 2?
s[s < 2].any()

結果:
True

# how many values < 2?
(s < 2).sum()

結果:
2
```

### 3.11 將序列重新索引
```
# sample series of five items
np.random.seed(123456)
s = pd.Series(np.random.randn(5))
s

結果:
0    0.469112
1   -0.282863
2   -1.509059
3   -1.135632
4    1.212112
dtype: float64

# change the index
s.index = ['a', 'b', 'c', 'd', 'e']
s

結果:
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
e    1.212112
dtype: float64

# a series that we will reindex
np.random.seed(123456)
s1 = pd.Series(np.random.randn(4), ['a', 'b', 'c', 'd'])
s1

結果:
a    0.469112
b   -0.282863
c   -1.509059
d   -1.135632
dtype: float64

# reindex with different number of labels
# results in dropped rows and/or NaN's
s2 = s1.reindex(['a', 'c', 'g'])
s2

結果:
a    0.469112
c   -1.509059
g         NaN
dtype: float64

# different types for the same values of labels
# causes big trouble
s1 = pd.Series([0, 1, 2], index=[0, 1, 2])
s2 = pd.Series([3, 4, 5], index=['0', '1', '2'])
s1 + s2

結果:
0   NaN
1   NaN
2   NaN
0   NaN
1   NaN
2   NaN
dtype: float64

# reindex by casting the label types
# and we will get the desired result
s2.index = s2.index.values.astype(int)
s1 + s2

結果:
0    3
1    5
2    7
dtype: int64

# fill with 0 instead of NaN
s2 = s.copy()
s2.reindex(['a', 'f'], fill_value=0)

結果:
a    0.469112
f    0.000000
dtype: float64

# create example to demonstrate fills
s3 = pd.Series(['red', 'green', 'blue'], index=[0, 3, 5])
s3

結果:
0      red
3    green
5     blue
dtype: object

# forward fill example
s3.reindex(np.arange(0,7), method='ffill')

結果:
0      red
1      red
2      red
3    green
4    green
5     blue
6     blue
dtype: object

# backwards fill example
s3.reindex(np.arange(0,7), method='bfill')

結果:
0      red
1    green
2    green
3    green
4     blue
5     blue
6      NaN
dtype: object
```
### 3.12 原地修改序列
```
# generate a Series to play with
np.random.seed(123456)
s = pd.Series(np.random.randn(3), index=['a', 'b', 'c'])
s

結果:
a    0.469112
b   -0.282863
c   -1.509059
dtype: float64

# change a value in the Series
# this is done in-place
# a new Series is not returned that has a modified value
s['d'] = 100
s

結果:
a      0.469112
b     -0.282863
c     -1.509059
d    100.000000
dtype: float64

# modify the value at 'd' in-place
s['d'] = -100
s

結果:
a      0.469112
b     -0.282863
c     -1.509059
d   -100.000000
dtype: float64

# remove a row / item
del(s['a'])
s

結果:
b     -0.282863
c     -1.509059
d   -100.000000
dtype: float64

copy = s.copy() # preserve s
slice = copy[:2] # slice with first two rows
slice

結果:
b   -0.282863
c   -1.509059
dtype: float64

# change item with label 10 to 1000
slice['b'] = 0
# and see it in the source
copy

結果:
b      0.000000
c     -1.509059
d   -100.000000
dtype: float64
```
