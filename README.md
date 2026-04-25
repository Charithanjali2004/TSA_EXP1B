# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data=pd.read_csv('DailyDelhiClimateTest.csv')
data.head()

data['date']=pd.to_datetime(data['date'])
data.set_index('date',inplace=True)

data_aggregated = data.groupby(data.index)['meanpressure'].mean().to_frame()

data_aggregated['meanpressure_diff']=data_aggregated['meanpressure']-data_aggregated['meanpressure'].shift(1)

data_aggregated['meanpressure_log'] = np.log(data_aggregated['meanpressure'].replace(0, 1e-9))
data_aggregated['meanpressure_log_diff']=data_aggregated['meanpressure_log']-data_aggregated['meanpressure_log'].shift(1)

result = seasonal_decompose(data_aggregated['meanpressure_log_diff'].dropna(), model='additive', period=12)
data_aggregated['meanpressure_log_seasonal_diff']=result.resid

plt.figure(figsize=(20, 24))

plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['meanpressure'], label='Original') 
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('date')
plt.ylabel('meanpressure')

plt.subplot(2, 1, 1)
plt.plot(data_aggregated['meanpressure_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('date')
plt.ylabel('meanpressure')

plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['meanpressure_log_seasonal_diff'], label='Log Transformation, Regular and Seasonal Differencing') 
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('date')
plt.ylabel('SDiff(RDiff(Log(meanpressure)))')

plt.subplot(2, 1, 1) 
plt.plot(data_aggregated['meanpressure_log'], label='Log Transformation') 
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('date')
plt.ylabel('Log(meanpressure)')

plt.subplot(1, 1, 1) 
plt.plot(data_aggregated['meanpressure_log_diff'], label='Log Transformation and Regular Differencing') 
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('date')
plt.ylabel('RDiff(Log(meanpressure))')

plt.subplot(1,1,1) 
plt.plot(data_aggregated['meanpressure_log_seasonal_diff'], label='Log Transformation and Regular Differencing and Seasonal Differencing')
plt.legend(loc='best')
plt.title('Seasonally Adjusted Data (Log Transformed and Differenced)') 
plt.xlabel('date')
plt.ylabel('SDiff(RDiff(Log(meanpressure)))') 
plt.tight_layout()
plt.show()
```
### OUTPUT:

<img width="1180" height="209" alt="image" src="https://github.com/user-attachments/assets/b02f21e8-530f-434b-90c0-6fb30b6fa83c" />


<img width="1185" height="103" alt="image" src="https://github.com/user-attachments/assets/4857e8d0-eb40-43ec-9c2a-f3bea13fc4e1" />


<img width="1135" height="337" alt="image" src="https://github.com/user-attachments/assets/6b5b4526-044e-468a-9c06-879a610775ff" />

REGULAR DIFFERENCING:

<img width="1182" height="359" alt="image" src="https://github.com/user-attachments/assets/8ff515e6-4ce6-4c0f-b500-ee8e1c228c33" />

SEASONAL ADJUSTMENT:

<img width="1181" height="592" alt="image" src="https://github.com/user-attachments/assets/760d70bb-74d6-4448-82b9-3ee00d1a9571" />

LOG TRANSFORMATION:

<img width="1175" height="332" alt="image" src="https://github.com/user-attachments/assets/2bd19372-58c8-4a5d-9289-adfb9ef5f258" />

<img width="1175" height="568" alt="image" src="https://github.com/user-attachments/assets/6f7c18b1-2919-408b-8fca-63012965b067" />

<img width="1138" height="567" alt="image" src="https://github.com/user-attachments/assets/33a218be-ffa6-4c07-bfb2-d1d6581e02d2" />


















### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
