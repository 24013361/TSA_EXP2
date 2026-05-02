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
A - LINEAR TREND ESTIMATION
```
import pandas as pd, numpy as np, matplotlib.pyplot as plt

df = pd.read_csv('/content/chennai_temperature_10years.csv',
                 parse_dates=['Date'], index_col='Date')

d = df['Temperature'].resample('YE').mean().to_frame()
d.index = d.index.year
d.reset_index(inplace=True)
d.rename(columns={'Date':'Year'}, inplace=True)

years = d['Year'].tolist()
temps = d['Temperature'].tolist()

X = [i - years[len(years)//2] for i in years]
n = len(years)

b = (n*sum(i*j for i,j in zip(X,temps)) - sum(temps)*sum(X)) / (n*sum(i*i for i in X) - sum(X)**2)
a = (sum(temps) - b*sum(X)) / n

trend = [a + b*i for i in X]

d['Linear Trend'] = trend
d.set_index('Year', inplace=True)

d['Temperature'].plot(kind='line', color='blue', marker='o')
d['Linear Trend'].plot(kind='line', color='black', linestyle='--')

plt.title('Linear Trend Estimation (Least Square Method)')
plt.xlabel('Year'); plt.ylabel('Temperature')
plt.legend(['Actual Temperature', f'Linear Trend: y={a:.2f}+{b:.2f}x'])
plt.grid(True); plt.tight_layout()
plt.show()
```
B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd, numpy as np, matplotlib.pyplot as plt

df = pd.read_csv('/content/chennai_temperature_10years.csv',
                 parse_dates=['Date'], index_col='Date')

d = df['Temperature'].resample('YE').mean().to_frame()
d.index = d.index.year
d.reset_index(inplace=True)
d.rename(columns={'Date':'Year'}, inplace=True)

years = d['Year'].tolist()
temps = d['Temperature'].tolist()

coeffs = np.polyfit(years, temps, 2)
trend = np.polyval(coeffs, years)

d['Polynomial Trend'] = trend
d.set_index('Year', inplace=True)

d['Temperature'].plot(kind='line', color='blue', marker='o')
d['Polynomial Trend'].plot(kind='line', color='black', linestyle='--')

plt.title('Polynomial Trend Estimation')
plt.xlabel('Year'); plt.ylabel('Temperature')
plt.legend(['Actual Temperature',
            f'y={coeffs[0]:.4f}x²+{coeffs[1]:.4f}x+{coeffs[2]:.2f}'])
plt.grid(True); plt.tight_layout()
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="642" height="473" alt="image" src="https://github.com/user-attachments/assets/ec8fd352-9d4c-471d-a154-f588a3c079fc" />

B- POLYNOMIAL TREND ESTIMATION
<img width="653" height="492" alt="image" src="https://github.com/user-attachments/assets/bda14aa5-e586-41b2-a745-c15a2876e47f" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
