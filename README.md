### Date: 28/08/2024
### Name: Ragul A C
### Register No:212221240042

## Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformation on measures Total revenue of mobile sales.
### ALGORITHM:
1. Load and Preprocess Data: Convert the Date column to datetime and sort by date.
2. Visualize Original Data: Plot TotalRevenue over time.
3. Log Transformation: Stabilize variance by applying the log transformation to TotalRevenue.
4. Differencing: Apply first differencing to remove trends.
5. ADF Test: Test stationarity using the ADF test.
6. Visualize Differenced Data: Plot the differenced log-transformed data.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller

## Load the Data
file_path = '/content/mobile_sales.csv'
data = pd.read_csv(file_path)

##Co nvert the Date column to datetime format and sort by date
data['Date'] = pd.to_datetime(data['Date'])
data = data.sort_values('Date')

## Visualize the original data
plt.figure(figsize=(12, 6))
plt.plot(data['Date'], data['TotalRevenue'], label='Original TotalRevenue')
plt.title('Original TotalRevenue Over Time')
plt.xlabel('Date')
plt.ylabel('TotalRevenue')
plt.grid(True)
plt.legend()
plt.show()

## Log transform the TotalRevenue (replace 0 values to avoid log(0) errors)
data['Log_TotalRevenue'] = np.log(data['TotalRevenue'].replace(0, np.nan))

# First differencing of the log-transformed data
data['Diff_Log_TotalRevenue'] = data['Log_TotalRevenue'].diff()

## Drop NaN values caused by differencing
diff_data = data.dropna(subset=['Diff_Log_TotalRevenue'])

## Perform Augmented Dickey-Fuller test on the differenced log-transformed data
adf_test = adfuller(diff_data['Diff_Log_TotalRevenue'])

## Print the ADF test results
adf_results = {
    'ADF Statistic': adf_test[0],
    'p-value': adf_test[1],
    'Used Lags': adf_test[2],
    'Number of Observations': adf_test[3],
    'Critical Values': adf_test[4],
    'Stationarity': 'Stationary' if adf_test[1] < 0.05 else 'Non-Stationary'
}

print('ADF Test Results:')
print('-----------------')
print('ADF Statistic:', adf_results['ADF Statistic'])
print('p-value:', adf_results['p-value'])
print('Used Lags:', adf_results['Used Lags'])
print('Number of Observations:', adf_results['Number of Observations'])
print('Critical Values:', adf_results['Critical Values'])
print('Conclusion:', adf_results['Stationarity'])

## Visualize the differenced data
plt.figure(figsize=(12, 6))
plt.plot(diff_data['Date'], diff_data['Diff_Log_TotalRevenue'], label='Differenced Log TotalRevenue', color='green')
plt.title('Differenced Log TotalRevenue Over Time')
plt.xlabel('Date')
plt.ylabel('Differenced Log TotalRevenue')
plt.grid(True)
plt.legend()
plt.show()
```

### OUTPUT:

REGULAR DIFFERENCING:
![download](https://github.com/user-attachments/assets/4244e34f-4847-4186-98b0-b3c9067b174f)




SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/330499bb-adf2-47fa-be45-c8265135591e)



LOG TRANSFORMATION:
![download](https://github.com/user-attachments/assets/6553a18b-a352-4906-aad2-58ebab5fd336)






### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on mobile sales data.
