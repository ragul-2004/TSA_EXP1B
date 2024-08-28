# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 05/03/2024

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
## Regular Differencing
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
data=pd.read_csv("/content/AirPassengers.csv",parse_dates=['Month'],index_col='Month')
data.head()
passengers['shifted_value']=passengers['#Passengers'].shift(1)
passengers['difference_value']=passengers['#Passengers']-passengers['shifted_value']
passengers.dropna(inplace=True)
print(passengers)
passengers.plot(kind='line')
```

## Seasonal Adjustment
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
data=pd.read_csv("/content/AirPassengers.csv",parse_dates=['Month'],index_col='Month')
passengers=pd.DataFrame(data)
result=seasonal_decompose(passengers['#Passengers'],model='additive',period=1)
seasonal=result.seasonal
passengers['Seasonal_value']=passengers['#Passengers']-seasonal
passengers.dropna(inplace=True)
print(passengers)
passengers.plot(kind='line')
```
## Log Transformation
```
import numpy as np
import pandas as pd
data= pd.read_csv('AirPassengers.csv')
data.head()
data.dropna(inplace=True)
x=data['Month']
y=data['#Passengers']
data_log=np.log(data['#Passengers'])
X=data['Month']
Y=data_log
import matplotlib.pyplot as plt
plt.plot(x,y)
plt.xlabel('Original Data')
plt.plot(X,Y)
plt.xlabel('Log- Transformed data')
```

### OUTPUT:

REGULAR DIFFERENCING:
![image](https://github.com/Vivekreddy8360/TSA_EXP1B/assets/94525701/e254bd66-541c-4c6b-ad70-55a6a16b1f19)



SEASONAL ADJUSTMENT:
![image](https://github.com/Vivekreddy8360/TSA_EXP1B/assets/94525701/4d0febe0-b100-456b-9a60-e6064f3bab15)


LOG TRANSFORMATION:
![image](https://github.com/Vivekreddy8360/TSA_EXP1B/assets/94525701/b33397ed-769e-4be4-9bbb-144dc4d61d81)
![image](https://github.com/Vivekreddy8360/TSA_EXP1B/assets/94525701/49a71ec2-d4bb-4ca2-91b8-e773e7d39acf)





### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
