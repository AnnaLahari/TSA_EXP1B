# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 27-04-2026

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

data = pd.read_csv("/content/Balaji Fast Food Sales.csv")

data.columns = data.columns.str.strip()

# Fix: Convert 'date' column to datetime and set it as the index
data['date'] = pd.to_datetime(data['date'], format='mixed')
data.set_index('date', inplace=True)

# Create the time series 'ts' from 'item_price', as requested by the user
ts = data['item_price'].resample('ME').mean().dropna()

ts_diff = ts - ts.shift(1)

result = seasonal_decompose(ts, model='additive', period=6)
ts_sea_diff = result.resid

ts_log = np.log(ts.replace(0, np.nan)).dropna()
ts_log_diff = ts_log - ts_log.shift(1)

result = seasonal_decompose(ts_log_diff.dropna(), model='additive', period=5)
ts_log_sea_diff = result.resid

# Plot 6 graphs
plt.figure(figsize=(12,10))

plt.subplot(6,1,1)
plt.plot(ts)
plt.title('Original time series')
plt.xlabel('date')
plt.ylabel('item_price')

plt.subplot(6,1,2)
plt.plot(ts_diff)
plt.title('Regular Differencing')
plt.xlabel('Release Date')
plt.ylabel('Differenced item_price')

plt.subplot(6,1,3)
plt.plot(ts_sea_diff)
plt.title('Seasonal Adjustment')
plt.xlabel('Release Date')
plt.ylabel('Seasonally Adjusted')


plt.subplot(6,1,4)
plt.plot(ts_log)
plt.title('Log Transformation')
plt.xlabel('Release Date')
plt.ylabel('Log(item_price))')

plt.subplot(6,1,5)
plt.plot(ts_log_diff)
plt.title('Log regular Differencing')
plt.xlabel('Release Date')
plt.ylabel('RDiff(Log)')

plt.subplot(6,1,6)
plt.plot(ts_log_sea_diff)
plt.title('Log seasonal adjustment')
plt.xlabel('Release Date')
plt.ylabel('SDiff(RDiff(Log))')

plt.tight_layout()
plt.show()
```
### OUTPUT:

ORIGINAL TIME SERIES:

<img width="1183" height="171" alt="image" src="https://github.com/user-attachments/assets/327cfabe-fa68-4b49-a8d6-959ea47f444e" />


DIFFERENCES SERIES:

<img width="1165" height="217" alt="image" src="https://github.com/user-attachments/assets/ec06ddb1-043d-49bb-b933-bf8ef1e4a5de" />


SEASONAL ADJUSTMENT:

<img width="1224" height="176" alt="image" src="https://github.com/user-attachments/assets/82b8a778-3432-42e7-917c-637add3a20bf" />


LOG TRANSFORMATION:

<img width="1185" height="167" alt="image" src="https://github.com/user-attachments/assets/9cd143d6-612f-4a33-afec-75b6f6d8ebf8" />


LOG REGULAR DIFFERENCING:

<img width="1206" height="170" alt="image" src="https://github.com/user-attachments/assets/da80b49c-9c68-4dc0-b766-354fa2d803fe" />


LOG SEASONAL ADJUSTMENT:

<img width="1199" height="173" alt="image" src="https://github.com/user-attachments/assets/a7662bf2-8a4c-4999-bfc5-a10e807f810f" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
