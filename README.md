# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
```
Name    : Jeshwanth Kumar P
Ref No. : 212223240114
Date    : 18-03-2025
```
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
### Load the dataset :
```
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt 
data = pd.read_csv('unq.csv')
data.head()
```
### Resampling data :
```
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

resampled_data = data.resample('Y').sum()
resampled_data.head()

resampled_data.index = resampled_data.index.year

resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Date':'Year'},inplace=True)

years = resampled_data['Year'].tolist()
prices = resampled_data['Close'].tolist()

resampled_data.head()

A - LINEAR TREND ESTIMATION

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, prices)]
n = len(years)
b = (n * sum(xy) - sum(prices) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(prices) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")

resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend

resampled_data['Prices']=prices
resampled_data['Prices'].plot(kind='line',color='blue',marker='o')
resampled_data['Linear Trend'].plot(kind='line',color='black',linestyle='--')
plt.title('Uniqlo Stock Prices with Linear Trend Estimation')
plt.xlabel('Year')
plt.ylabel('Closing Prices')
plt.legend()
plt.show()


B- POLYNOMIAL TREND ESTIMATION

print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")
resampled_data['Prices'].plot(kind='line',color='blue',marker='o')
resampled_data['Polynomial Trend'].plot(kind='line',color='black',marker='o')
plt.title('Uniqlo Stock Prices with Polynomial Trend Estimation')
plt.xlabel('Year')
plt.ylabel('CLosing Prices')
plt.legend()
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION

![image](https://github.com/user-attachments/assets/fb9c0e7c-9660-4dc7-b1ce-0009ace6ccc3)


B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/5b708f58-48b0-4dc2-8d77-16dc4142ba53)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
