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
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv('Automobile.csv')

# Group by model_year and calculate average mpg per year
resampled_data = data.groupby('model_year')['mpg'].mean().reset_index()

# Extract years and mpg values
years = resampled_data['model_year'].tolist()
mpg = resampled_data['mpg'].tolist()

# Center X values around the middle year
X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, mpg)]
n = len(years)

# Linear regression calculation
b = (n * sum(xy) - sum(mpg) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(mpg) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]

# Polynomial regression (2nd degree)
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, mpg)]
coeff = [[len(X), sum(X), sum(x2)], [sum(X), sum(x2), sum(x3)], [sum(x2), sum(x3), sum(x4)]]
Y = [sum(mpg), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]

# Print equations
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"Polynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

# Add trends to dataframe
resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend

# Plot Linear Trend
plt.figure(figsize=(10,6))
plt.plot(resampled_data['model_year'], resampled_data['mpg'], 'bo-', label='Average MPG')
plt.plot(resampled_data['model_year'], resampled_data['Linear Trend'], 'k--', label='Linear Trend')
plt.xlabel('Model Year')
plt.ylabel('Average MPG')
plt.title('Linear Trend of Average MPG over Model Years')
plt.legend()
plt.grid(True)
plt.show()

# Plot Polynomial Trend
plt.figure(figsize=(10,6))
plt.plot(resampled_data['model_year'], resampled_data['mpg'], 'bo-', label='Average MPG')
plt.plot(resampled_data['model_year'], resampled_data['Polynomial Trend'], 'r-', label='Polynomial Trend')
plt.xlabel('Model Year')
plt.ylabel('Average MPG')
plt.title('Polynomial Trend of Average MPG over Model Years')
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT
<img width="335" height="40" alt="image" src="https://github.com/user-attachments/assets/9dcb0c12-f647-430b-992b-12a82980daf2" /><br>

A - LINEAR TREND ESTIMATION
<img width="884" height="545" alt="image" src="https://github.com/user-attachments/assets/a96cd94a-28eb-47ac-9795-8a72315dc686" /><br>

B- POLYNOMIAL TREND ESTIMATION
<img width="866" height="546" alt="image" src="https://github.com/user-attachments/assets/ab92c3cb-9d12-4c5b-87b4-881c022a67e6" /><br>

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
