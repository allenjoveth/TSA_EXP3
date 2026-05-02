# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 02.05.2026

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
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv('/content/Video_Games_Sales.csv')

# Convert Year column
df['Year_of_Release'] = pd.to_datetime(df['Year_of_Release'], format='%Y', errors='coerce')

# Remove missing values
df = df.dropna(subset=['Year_of_Release', 'Global_Sales'])

# Group by year (important for time series)
yearly_sales = df.groupby('Year_of_Release')['Global_Sales'].sum()

# Convert to numpy array
data = yearly_sales.values

# Parameters
N = len(data)
lags = range(min(20, N))

autocorr_values = []

# Mean and Variance
mean_data = np.mean(data)
variance_data = np.var(data)

# ACF Calculation
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((data[:-lag] - mean_data) * (data[lag:] - mean_data)) / N
        autocorr_values.append(auto_cov / variance_data)

# Plot ACF
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)

plt.title('Autocorrelation Function (ACF) - Video Game Sales')
plt.xlabel('Lag (Years)')
plt.ylabel('Autocorrelation')

plt.grid(True)
plt.show()

```

### OUTPUT:

<img width="999" height="618" alt="image" src="https://github.com/user-attachments/assets/e0e1c1e9-ce27-4363-8267-3704b0fd1e5e" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
