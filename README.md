# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:03/11/2026.

Data set : Tesla stock price.
### AIM:
To implement Linear and Polynomial Trend Estimation using Python on the Tesla stock price dataset to identify and analyze the trends in stock prices

### ALGORITHM:
1.Import the necessary libraries such as NumPy, Pandas and Matplotlib.

2.Load the Tesla stock price dataset using Pandas.

3.Extract the date and closing price columns from the dataset.

4.Convert the date column into a numerical format for trend estimation.

5.Calculate the linear trend values using the Least Squares Method.

6.Calculate the polynomial trend values using the Polynomial Fitting Method.

7.Plot the actual Tesla stock prices along with the estimated linear and polynomial trends.

8.Display the graphs and end the program.
### PROGRAM:
A - LINEAR TREND ESTIMATION

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("/content/TSLA.csv")

# Adjust columns for TSLA dataset (using 'Date' and 'Close')
df["Date"] = pd.to_datetime(df["Date"])
df = df.dropna(subset=["Close"])

df = df.reset_index(drop=True)

period = df["Date"]
close_prices = df["Close"].tolist()

n = len(close_prices)

X = [i - n//2 for i in range(n)]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, close_prices)]

b = (n*sum(xy) - sum(close_prices)*sum(X)) / (n*sum(x2) - (sum(X)**2))
a = (sum(close_prices) - b*sum(X)) / n

linear_trend = [a + b*X[i] for i in range(n)]

print("Linear Trend Equation")
print(f"y = {a:.2f} + ({b:.2f})X")

plt.figure(figsize=(12,6))
plt.plot(period, close_prices, label="Close Price", alpha=0.7)
plt.plot(period, linear_trend, 'k--', linewidth=2, label="Linear Trend")

plt.title("Tesla Stock Close Price Linear Trend Estimation")
plt.xlabel("Date")
plt.ylabel("Close Price (USD)")
plt.legend()
plt.grid(True)
plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Changed to read the available TSLA dataset
df = pd.read_csv("/content/TSLA.csv")

# Using 'Date' and 'Close' columns which are present in TSLA.csv
df["Date"] = pd.to_datetime(df["Date"])
df = df.dropna(subset=["Close"])

df = df.reset_index(drop=True)

period = df["Date"]
close_prices = df["Close"].tolist()

n = len(close_prices)

X = [i - n//2 for i in range(n)]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, close_prices)]

x3 = [i**3 for i in X]

x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, close_prices)]

coeff = [
    [n, sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [
    sum(close_prices),
    sum(xy),
    sum(x2y)
]

A = np.array(coeff)
B = np.array(Y)

a_poly, b_poly, c_poly = np.linalg.solve(A, B)

poly_trend = [
    a_poly + b_poly*X[i] + c_poly*(X[i]**2)
    for i in range(n)
]

print("Polynomial Trend Equation")
print(f"y = {a_poly:.2f} + ({b_poly:.2f})X + ({c_poly:.2f})X²")

plt.figure(figsize=(12,6))
plt.plot(period, close_prices, label="Close Price", alpha=0.7)
plt.plot(period, poly_trend, 'r--', linewidth=2, label="Polynomial Trend")

plt.title("Tesla Stock Close Price Polynomial Trend Estimation")
plt.xlabel("Date")
plt.ylabel("Close Price (USD)")
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="911" height="459" alt="image" src="https://github.com/user-attachments/assets/8a0032f3-fd5c-473d-bceb-7da0981d7c8b" />


B- POLYNOMIAL TREND ESTIMATION
<img width="952" height="466" alt="image" src="https://github.com/user-attachments/assets/590cf09e-8a6f-4518-9829-81cb33ccd346" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
