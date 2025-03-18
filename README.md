# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
#### Load the dataset:
```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
df=pd.read_csv('unq.csv')
df.head()
```
#### Resampling data:
```
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)
resampled_data = df.resample('YE').mean()[['Close']]
resampled_data.reset_index(inplace=True)

resampled_data.rename(columns={'Date': 'Year'}, inplace=True)
resampled_data['Year'] = resampled_data['Year'].dt.year

resampled_data

years = resampled_data['Year'].tolist()
prices = resampled_data['Close'].tolist()

X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, prices)]

n = len(years)
b = (n * sum(xy) - sum(prices) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(prices) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, prices)]

coeff = [[len(X), sum(X), sum(x2)],
[sum(X), sum(x2), sum(x3)],
[sum(x2), sum(x3), sum(x4)]]
Y = [sum(prices), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")
```

####  A - LINEAR TREND ESTIMATION
```
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
```

#### B- POLYNOMIAL TREND ESTIMATION 

```
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

![image](https://github.com/user-attachments/assets/b2ce4f4b-c25c-4c07-8a73-5ad77913043a)


B- POLYNOMIAL TREND ESTIMATION

![image](https://github.com/user-attachments/assets/b7f6959e-56ab-4cd1-ab46-68ce5569a2a3)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
