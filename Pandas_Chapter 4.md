### Chapter 4：用資料框表示表格及多變數資料
### 4.1 設定pandas
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
```
### 4.2 建立資料框物件
### 4.2.1 使用NumPy函數的結果建立資料框
```
# From a 1-d array
pd.DataFrame(np.arange(1, 6))

結果:
   0
0  1
1  2
2  3
3  4
4  5

# create a DataFrame from a 2-d ndarray
df = pd.DataFrame(np.array([[10, 11], [20, 21]]))
df

結果:
    0   1
0  10  11
1  20  21

# retrieve the columns index
df.columns

結果:
RangeIndex(start=0, stop=2, step=1)

# specify column names
df = pd.DataFrame(np.array([[70, 71], [90, 91]]),
                  columns=['Missoula', 'Philadelphia'])
df

結果:
   Missoula  Philadelphia
0        70            71
1        90            91

# how many rows?
len(df)

結果:
2

# what is the dimensionality
df.shape

結果:
(2,2)
```
### 4.2.2使用Python字典及pandas序列物件建立資料框
```
# initialization using a python dictionary
temps_missoula = [70, 71]
temps_philly = [90, 91]
temperatures = {'Missoula': temps_missoula,
                'Philadelphia': temps_philly}
pd.DataFrame(temperatures)

結果:
   Missoula  Philadelphia
0        70            90
1        71            91

# create a DataFrame for a list of Series objects
temps_at_time0 = pd.Series([70, 90])
temps_at_time1 = pd.Series([71, 91])
df = pd.DataFrame([temps_at_time0, temps_at_time1])
df

結果:
    0   1
0  70  90
1  71  91

# try to specify column names
df = pd.DataFrame([temps_at_time0, temps_at_time1],
                  columns=['Missoula', 'Philadelphia'])
df

結果:
   Missoula  Philadelphia
0       NaN           NaN
1       NaN           NaN

# specify names of columns after creation
df = pd.DataFrame([temps_at_time0, temps_at_time1])
df.columns = ['Missoula', 'Philadelphia']
df

結果:
   Missoula  Philadelphia
0        70            90
1        71            91

# construct using a dict of Series objects
temps_mso_series = pd.Series(temps_missoula)
temps_phl_series = pd.Series(temps_philly)
df = pd.DataFrame({'Missoula': temps_mso_series,
                   'Philadelphia': temps_phl_series})
df

結果:
   Missoula  Philadelphia
0        70            90
1        71            91

# alignment occurs during creation
temps_nyc_series = pd.Series([85, 87], index=[1, 2])
df = pd.DataFrame({'Missoula': temps_mso_series,
                   'Philadelphia': temps_phl_series,
                   'New York': temps_nyc_series})
df

結果:
   Missoula  New York  Philadelphia
0      70.0       NaN          90.0
1      71.0      85.0          91.0
2       NaN      87.0           NaN
```
### 4.2.3從CSV檔案建立資料框
```
# read in the data and print the first five rows
# use the Symbol column as the index, and 
# only read in columns in positions 0, 2, 3, 7
sp500 = pd.read_csv("data/sp500.csv", 
                    index_col='Symbol', 
                    usecols=[0, 2, 3, 7])
                    
# peek at the first 5 rows of the data using .head()
sp500.head()

結果:
                        Sector   Price  Book Value
Symbol                                            
MMM                Industrials  141.14      26.668
ABT                Health Care   39.60      15.573
ABBV               Health Care   53.95       2.954
ACN     Information Technology   79.79       8.326
ACE                 Financials  102.91      86.897

# how many rows of data?  Should be 500
len(sp500)

結果:
500

# what is the shape?
sp500.shape

結果:
(500, 3)

# what is the size?
sp500.size

結果:
1500

# examine the index
sp500.index

結果:
Index(['MMM', 'ABT', 'ABBV', 'ACN', 'ACE', 'ACT', 'ADBE', 'AES', 'AET', 'AFL',
       ...
       'XEL', 'XRX', 'XLNX', 'XL', 'XYL', 'YHOO', 'YUM', 'ZMH', 'ZION', 'ZTS'],
      dtype='object', name='Symbol', length=500)
      
# get the columns
sp500.columns

結果:
Index(['Sector', 'Price', 'Book Value'], dtype='object')
```
### 4.3 存取資料框的資料
### 4.3.1選擇資料框的行
```
# retrieve the Sector column
sp500['Sector'].head()

結果:
Symbol
MMM                Industrials
ABT                Health Care
ABBV               Health Care
ACN     Information Technology
ACE                 Financials
Name: Sector, dtype: object

type(sp500['Sector'])

結果:
pandas.core.series.Series

# retrieve the Price and Book Value columns
sp500[['Price', 'Book Value']].head()

結果:
         Price  Book Value
Symbol                    
MMM     141.14      26.668
ABT      39.60      15.573
ABBV     53.95       2.954
ACN      79.79       8.326
ACE     102.91      86.897

# show that this is a DataFrame
type(sp500[['Price', 'Book Value']])

結果:
pandas.core.frame.DataFrame

# attribute access of column by name
sp500.Price

結果:
Symbol
MMM     141.14
ABT      39.60
ABBV     53.95
ACN      79.79
ACE     102.91
         ...  
YHOO     35.02
YUM      74.77
ZMH     101.84
ZION     28.43
ZTS      30.53
Name: Price, Length: 500, dtype: float64
```
### 4.3.2選取資料框的列
```
# get row with label MMM
# returned as a Series
sp500.loc['MMM']

結果:
Sector        Industrials
Price              141.14
Book Value         26.668
Name: MMM, dtype: object

# rows with label MMM and MSFT
# this is a DataFrame result
sp500.loc[['MMM', 'MSFT']]

結果:
                        Sector   Price  Book Value
Symbol                                            
MMM                Industrials  141.14      26.668
MSFT    Information Technology   40.12      10.584

# get rows in location 0 and 2
sp500.iloc[[0, 2]]

結果:
             Sector   Price  Book Value
Symbol                                 
MMM     Industrials  141.14      26.668
ABBV    Health Care   53.95       2.954

# get the location of MMM and A in the index
i1 = sp500.index.get_loc('MMM')
i2 = sp500.index.get_loc('A')
(i1, i2)

結果:
(0, 10)

# and get the rows
sp500.iloc[[i1, i2]]

結果:
             Sector   Price  Book Value
Symbol                                 
MMM     Industrials  141.14      26.668
A       Health Care   56.18      16.928
```
### 4.3.3利用.at[]及.iat[]，以標籤或位置進行純量查詢
```
# by label in both the index and column
sp500.at['MMM', 'Price']

結果:
141.13999999999999

# by location.  Row 0, column 1
sp500.iat[0, 1]

結果:
141.13999999999999
```
### 4.3.4使用[]運算子切割
```
# first five rows
sp500[:5]

結果:
                        Sector   Price  Book Value
Symbol                                            
MMM                Industrials  141.14      26.668
ABT                Health Care   39.60      15.573
ABBV               Health Care   53.95       2.954
ACN     Information Technology   79.79       8.326
ACE                 Financials  102.91      86.897

# ABT through ACN labels
sp500['ABT':'ACN']

結果:
                        Sector  Price  Book Value
Symbol                                           
ABT                Health Care  39.60      15.573
ABBV               Health Care  53.95       2.954
ACN     Information Technology  79.79       8.326
```
### 4.4 利用布林選擇選取列
```
# what rows have a price < 100?
sp500.Price < 100

結果:
Symbol
MMM     False
ABT      True
ABBV     True
ACN      True
ACE     False
        ...  
YHOO     True
YUM      True
ZMH     False
ZION     True
ZTS      True
Name: Price, Length: 500, dtype: bool

# now get the rows with Price < 100
sp500[sp500.Price < 100]

結果:
                        Sector  Price  Book Value
Symbol                                           
ABT                Health Care  39.60      15.573
ABBV               Health Care  53.95       2.954
ACN     Information Technology  79.79       8.326
ADBE    Information Technology  64.30      13.262
AES                  Utilities  13.61       5.781
...                        ...    ...         ...
XYL                Industrials  38.42      12.127
YHOO    Information Technology  35.02      12.768
YUM     Consumer Discretionary  74.77       5.147
ZION                Financials  28.43      30.191
ZTS                Health Care  30.53       2.150

[407 rows x 3 columns]

# get only the Price where Price is < 10 and > 0
r = sp500[(sp500.Price < 10) & 
          (sp500.Price > 6)] ['Price']
r

結果:
Symbol
HCBK    9.80
HBAN    9.10
SLM     8.82
WIN     9.38
Name: Price, dtype: float64

# price > 100 and in the Health Care Sector
r = sp500[(sp500.Sector == 'Health Care') & 
          (sp500.Price > 100.00)] [['Price', 'Sector']]
r

結果:
         Price       Sector
Symbol                     
ACT     213.77  Health Care
ALXN    162.30  Health Care
AGN     166.92  Health Care
AMGN    114.33  Health Care
BCR     146.62  Health Care
...        ...          ...
REGN    297.77  Health Care
TMO     115.74  Health Care
WAT     100.54  Health Care
WLP     108.82  Health Care
ZMH     101.84  Health Care

[19 rows x 2 columns]
```
### 4.5 跨越行與列進行選取
```
# select the price and sector columns for ABT and ZTS
sp500.loc[['ABT', 'ZTS']][['Sector', 'Price']]

結果:
             Sector  Price
Symbol                    
ABT     Health Care  39.60
ZTS     Health Care  30.53
```
