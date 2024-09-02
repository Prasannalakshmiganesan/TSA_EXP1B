### Developed By: Prasannalakshmi G
### Reg No: 212222240075
### Date: 

# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA


### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international goodreads books dataset

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("Goodreadsbooks.csv", nrows = 10)
train.timestamp = pd.to_datetime(train.publication_date, format = '%m/%d/%Y')
train.drop('publication_date', axis=1, inplace = True)
train.head()
train['bookID'].plot()

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)

adf_test(train['bookID'])


train['book_ID_diff'] = train['bookID'] - train['bookID'].shift(1)
train['book_ID_diff'].dropna().plot()

# Seasonal Differencing
n=7
train['book_ID_diff'] = train['bookID'] - train['bookID'].shift(n)
train['book_ID_diff'].dropna().plot()

# Transformation
train['bookID_log'] = np.log(train['bookID'])
train['bookID_log_diff'] = train['bookID_log'] - train['bookID_log'].shift(1)
train['bookID_log_diff'].dropna().plot()


```

### OUTPUT:
![image](https://github.com/user-attachments/assets/e07232a3-30b5-45da-a7c6-784c40c8ba93)

![image](https://github.com/user-attachments/assets/ee19eee7-d92c-41a2-bf9a-ee1ea641b375)

REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/26e34c12-29d6-406f-b083-6f81e13023ca)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/6ac770b1-9f0e-4bcb-bb03-ac6b7801f1a6)

LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/d3ed1812-2963-4af9-93a2-b5ac3e7bbc19)


ALL 3:

![image](https://github.com/user-attachments/assets/28df4fd3-ca24-47c8-8805-fe6c5318cf2a)



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international goodreads books dataset
data.
