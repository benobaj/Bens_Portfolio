# Hourly Energy Consumption

## Step 1 :

### Import Library


```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

%matplotlib inline
```


## Step 2

### Get to know about your dataset


```python
df = pd.read_csv("/Users/macbookpro/Desktop/tableau/Jupyter Data /Hourly Energy Consumption/AEP_hourly.csv",parse_dates=["Datetime"]) 
df.head(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Datetime</th>
      <th>AEP_MW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2004-12-31 01:00:00</td>
      <td>13478.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2004-12-31 02:00:00</td>
      <td>12865.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AEP_MW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>121273.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>15499.513717</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2591.399065</td>
    </tr>
    <tr>
      <th>min</th>
      <td>9581.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>13630.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>15310.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>17200.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>25695.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 121273 entries, 0 to 121272
    Data columns (total 2 columns):
     #   Column    Non-Null Count   Dtype         
    ---  ------    --------------   -----         
     0   Datetime  121273 non-null  datetime64[ns]
     1   AEP_MW    121273 non-null  float64       
    dtypes: datetime64[ns](1), float64(1)
    memory usage: 1.9 MB



```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Datetime</th>
      <th>AEP_MW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2004-12-31 01:00:00</td>
      <td>13478.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2004-12-31 02:00:00</td>
      <td>12865.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2004-12-31 03:00:00</td>
      <td>12577.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2004-12-31 04:00:00</td>
      <td>12517.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2004-12-31 05:00:00</td>
      <td>12670.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>121268</th>
      <td>2018-01-01 20:00:00</td>
      <td>21089.0</td>
    </tr>
    <tr>
      <th>121269</th>
      <td>2018-01-01 21:00:00</td>
      <td>20999.0</td>
    </tr>
    <tr>
      <th>121270</th>
      <td>2018-01-01 22:00:00</td>
      <td>20820.0</td>
    </tr>
    <tr>
      <th>121271</th>
      <td>2018-01-01 23:00:00</td>
      <td>20415.0</td>
    </tr>
    <tr>
      <th>121272</th>
      <td>2018-01-02 00:00:00</td>
      <td>19993.0</td>
    </tr>
  </tbody>
</table>
<p>121273 rows × 2 columns</p>
</div>




```python
df["New_tate"]=pd.to_datetime(df["Datetime"]).dt.date
df["New_time"]=pd.to_datetime(df["Datetime"]).dt.time
df["Year"]=pd.to_datetime(df["Datetime"]).dt.year
df["Month"]=pd.to_datetime(df["Datetime"]).dt.month 
df.head(4)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Datetime</th>
      <th>AEP_MW</th>
      <th>New_Date</th>
      <th>New_time</th>
      <th>Year</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2004-12-31 01:00:00</td>
      <td>13478.0</td>
      <td>2004-12-31</td>
      <td>01:00:00</td>
      <td>2004</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2004-12-31 02:00:00</td>
      <td>12865.0</td>
      <td>2004-12-31</td>
      <td>02:00:00</td>
      <td>2004</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2004-12-31 03:00:00</td>
      <td>12577.0</td>
      <td>2004-12-31</td>
      <td>03:00:00</td>
      <td>2004</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2004-12-31 04:00:00</td>
      <td>12517.0</td>
      <td>2004-12-31</td>
      <td>04:00:00</td>
      <td>2004</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["Year"].unique()
```




    array([2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014,
           2015, 2016, 2017, 2018])




```python
df["Year"].nunique()
```




    15



## Maximum Energy Consumes in Year 2018


```python
df[df["Year"]==2018]["AEP_MW"]
```




    107401    18687.0
    116138    13286.0
    116139    12587.0
    116140    12296.0
    116141    12059.0
               ...   
    121268    21089.0
    121269    20999.0
    121270    20820.0
    121271    20415.0
    121272    19993.0
    Name: AEP_MW, Length: 5136, dtype: float64




```python
df[df["Year"]==2018]["AEP_MW"].max()
```




    22759.0



# Minimum Energy Consumes in Year 2018


```python
df[df["Year"]==2018]["AEP_MW"].min()
```




    9815.0



# Average Energy Consumes in Year 2018


```python
df[df["Year"]==2018]["AEP_MW"].mean()
```




    15290.612733644859



# Energy Distribution Using Kernel Density Estimation


```python
sns.distplot(df["AEP_MW"])
```

    /Users/macbookpro/opt/anaconda3/lib/python3.9/site-packages/seaborn/distributions.py:2619: FutureWarning: `distplot` is a deprecated function and will be removed in a future version. Please adapt your code to use either `displot` (a figure-level function with similar flexibility) or `histplot` (an axes-level function for histograms).
      warnings.warn(msg, FutureWarning)





    <AxesSubplot:xlabel='AEP_MW', ylabel='Density'>






    
![png](HourlyEnergyConsumption_files/HourlyEnergyConsumption_21_2.png)
    



#  Energy Consumption in 15 Years


```python
sns.lineplot(x=df["Year"],y=df["AEP_MW"],data=df)
```




    <AxesSubplot:xlabel='Year', ylabel='AEP_MW'>






    
![png](HourlyEnergyConsumption_files/HourlyEnergyConsumption_23_1.png)
    



#  Average in Energy Consumption in 2018 


```python
df[df["Year"]==2018]["AEP_MW"].mean()
```




    15290.612733644859




```python
df[df["Year"]==2018]["AEP_MW"].plot.line()
```




    <AxesSubplot:>






    
![png](HourlyEnergyConsumption_files/HourlyEnergyConsumption_26_1.png)
    




```python
sns.jointplot(x=df["Year"],
            y=df["AEP_MW"],
             data=df,
            kind="kde")
```




    <seaborn.axisgrid.JointGrid at 0x7fddf05011c0>






    
![png](HourlyEnergyConsumption_files/HourlyEnergyConsumption_27_1.png)
    


