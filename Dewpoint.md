```python
import pandas as pd
import numpy as np

# Load the data
data_df = pd.read_excel("D:/air quality/OneDrive - design.iitd.ac.in/Desktop/Jodhpur_TB/Jodhpur_original/Raw_data/all_raw_new_hourly_shifted.xlsx")

# Constants for dew point calculation
a = 17.27
b = 237.7

# Ambient temperature and relative humidity
T = data_df['Filter_Temperature']
RH = data_df['Filter_Humidity'] / 100  # Assuming humidity is given in percentage

# Alpha calculation
alpha = (a * T) / (b + T) + np.log(RH)

# Dew point calculation
dew_point = (b * alpha) / (a - alpha)

# Add the Dew_Point to the DataFrame for display
data_df['Dew_Point'] = dew_point

# Compare dew point with Filter_Temperature and create a new column with values "wet" or "dry"
data_df['Condition'] = np.where(data_df['Enclosure_Temperature'] <= dew_point, 'wet', 'dry')

# Display the first few rows including the new Condition column
# data_df[['Temperature', 'Humidity', 'Filter_Temperature', 'Dew_Point', 'Condition']].head()
data_df.to_excel('drywet_jodhpur_enclo_fil.xlsx',index=False)
```
