```python
import pandas as pd
import os
import numpy as np
# Load the file
df= pd.read_excel("C:/Users/gulsh/Downloads/pkcombined.xlsx")
# If datetime is splitted into date and time
df['time']= df['time'].astype(str)
df['date']=df['date'].astype(str)
# convert and join
df['datetime']= pd.to_datetime(df['date']+' '+df['time'])
df=df.drop(['date','time'],axis=1)
# average based on required frequency
df = df.resample(rule='60Min', on='datetime').mean()
# saving file, dont use index=False
df.to_excel("C:/Users/gulsh/Downloads/pk2_combined_hourly.xlsx")
df
```
