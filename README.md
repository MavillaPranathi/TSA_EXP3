### Developed by : M.Pranathi
### Register no : 212222240064
# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
df=pd.read_csv('supermarketsales.csv')
df.head()

# Convert 'Date' to datetime and set it as index
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)

# 1. Find the mean and variance of 'Total'
mean_total = np.mean(df['Total'])
variance_total = np.var(df['Total'])

print(f"Mean of Total Sales: {mean_total}")
print(f"Variance of Total Sales: {variance_total}")

# 2. Implement normalization (z-score normalization)
df['Total_normalized'] = (df['Total'] - mean_total) / np.sqrt(variance_total)

# 3. Compute autocorrelation function (ACF) manually for the first 35 lags
def autocorrelation(series, lag):
    n = len(series)
    mean_series = np.mean(series)
    var_series = np.var(series)
    
    autocorr = 0
    for i in range(n - lag):
        autocorr += (series[i] - mean_series) * (series[i + lag] - mean_series)
    
    return autocorr / ((n - lag) * var_series)

# Compute autocorrelation for lags 0 through 35
acf_values = [autocorrelation(df['Total_normalized'], lag) for lag in range(36)]

# 4. Store results in an array
acf_array = np.array(acf_values)

# 5. Represent the results graphically (ACF plot)
plt.figure(figsize=(10, 6))
plt.stem(range(36), acf_array, use_line_collection=True)
plt.title('Autocorrelation Function (ACF) for Normalized Total Sales')
plt.xlabel('Lag')
plt.ylabel('ACF')
plt.grid(True)
plt.show()

```

### OUTPUT:

![image](https://github.com/user-attachments/assets/578de42c-0e61-46f6-bd31-13e163a2623e)

![image](https://github.com/user-attachments/assets/39fac4ee-c9ea-40f6-9b18-a32ba8127dd2)

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
