# Divide-big-volume-data-according-to-year
Process 4366298 rows csv

A csv file contains 4,366,298 rows x 11 columns, the type of each columns as below.
 #   Column          Dtype  
---  ------          -----  
 0   pid             int64  
 1   datatime        object 
 2   measuretime     int64  
 3   sbp             int64  
 4   dbp             int64  
 5   dia_temp_value  float64
 6   conductivity    float64
 7   uf              float64
 8   blood_flow      float64
 9   time            int64  
dtypes: float64(4), int64(5), object(1)

Cause excel only support 1,048,576 rows by 16,384 columns, the file cannot be opened properly thus cannot process accordingly in excel. 

The solution is to divide data in Python according to Year(2013-09-04 00:05:46). 

1. Convert [datatime] type from object to datetime64[ns], in order to use the pd.to_datetime.

df_vip['datatime']=pd.to_datetime(df_vip['datatime'],errors='coerce')

2. Add a column to extract Year

import pandas as pd
import numpy as np
import time
s=time.time()
df_vip['date'] =df_vip['datatime'].dt.date
print(df_vip)

3. Divide the big volume data based on Year

import datetime as dt
df_vip1=df_vip[df_vip['date'].dt.year == 2014]
print(df_vip1)

