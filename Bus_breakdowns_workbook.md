

```python
#imports libraries and csv file
import pandas as pd
import numpy as np
df = pd.read_csv('bus-breakdown-and-delays.csv')
#pd.set_option('display.max_rows', 5000)
```

    /anaconda3/lib/python3.6/site-packages/IPython/core/interactiveshell.py:2728: DtypeWarning: Columns (17) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)


https://www.kaggle.com/new-york-city/ny-bus-breakdown-and-delays

- Change column titles case
- format how_long_delayed column
- some states in Boro column, should be split
- 1 line of 2019-2020 in school year. Mistake?
- Bus Companies multiple under different names


```python
#changes column titles case
df.columns = df.columns.str.lower()
```


```python
#changes case
df['how_long_delayed'] = df['how_long_delayed'].str.lower()
#changes formatting
df['how_long_delayed'] = df['how_long_delayed'].str.replace('145h', '8700')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('100h', '6000')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1h', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('hr1', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1ho', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('halfhour', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('3omin', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('3omins', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2hr', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2hour', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hoiur', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('one hour', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('hour', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hr', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45hr', '2700')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hour15m', '75')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hr', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hour', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hours', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hrs', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hour', '60')
```


```python
#eliminates unnecessary characters
df['how_long_delayed'] = df.how_long_delayed.str.replace('[a-zA-Z]', '')
#changes characters
df['how_long_delayed'] = df['how_long_delayed'].str.replace(' ', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('.', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace(':', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('to', '-')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('/', '-')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('+', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace(',', '')
#changes values
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1.5', '90')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('16-30', '20')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('31-45', '40')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('46-60', '50')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('0-15', '10')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('5-10', '8')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('15-20', '18')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('15-30', '23')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('10-20', '28')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('10-15', '13')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('15-25', '20')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('10-12', '11')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('61-90', '75')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('20-30', '25')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('20-25', '28')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('30-60', '45')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('3060', '45')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('30-35', '33')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('30-40', '35')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('30-45', '40')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('35-40', '38')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('35-45', '40')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('40-45', '43')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('25-30', '28')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('25-35', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('20-25', '28')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45-1', '50')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45-50', '48')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45-60', '53')
```


```python
df['occurred_on'].str.replace('T', '')
df['created_on'].str.replace('T', '')
df['informed_on'].str.replace('T', '')
df['last_updated_on'].str.replace('T', '')
```




    0         2015-09-0206:29:16
    1         2015-09-0206:30:19
    2         2015-09-0208:05:39
    3         2015-09-0207:02:01
    4         2015-09-0207:04:25
    5         2015-09-0207:14:33
    6         2015-09-0207:22:39
    7         2015-09-0207:29:44
    8         2015-09-0207:51:02
    9         2015-09-0207:56:00
    10        2015-09-0208:01:24
    11        2015-09-0208:04:17
    12        2015-09-0208:05:40
    13        2015-09-0208:06:23
    14        2015-09-0807:55:15
    15        2015-09-0807:55:28
    16        2015-09-0807:57:17
    17        2015-09-2508:02:53
    18        2015-09-2508:10:23
    19        2015-09-2506:44:22
    20        2015-09-2508:09:50
    21        2015-09-0808:00:48
    22        2015-09-0808:01:48
    23        2015-09-0808:05:37
    24        2015-09-0808:01:54
    25        2015-09-0808:02:21
    26        2015-09-0808:02:28
    27        2015-09-0808:02:44
    28        2015-09-0906:35:12
    29        2015-09-0906:35:41
                     ...        
    250594    1900-01-0100:00:00
    250595    1900-01-0100:00:00
    250596    1900-01-0100:00:00
    250597    1900-01-0100:00:00
    250598    1900-01-0100:00:00
    250599    1900-01-0100:00:00
    250600    1900-01-0100:00:00
    250601    1900-01-0100:00:00
    250602    1900-01-0100:00:00
    250603    1900-01-0100:00:00
    250604    1900-01-0100:00:00
    250605    1900-01-0100:00:00
    250606    1900-01-0100:00:00
    250607    1900-01-0100:00:00
    250608    1900-01-0100:00:00
    250609    1900-01-0100:00:00
    250610    1900-01-0100:00:00
    250611    1900-01-0100:00:00
    250612    1900-01-0100:00:00
    250613    1900-01-0100:00:00
    250614    1900-01-0100:00:00
    250615    1900-01-0100:00:00
    250616    1900-01-0100:00:00
    250617    1900-01-0100:00:00
    250618    1900-01-0100:00:00
    250619    1900-01-0100:00:00
    250620    2018-10-1506:04:30
    250621    1900-01-0100:00:00
    250622    1900-01-0100:00:00
    250623    1900-01-0100:00:00
    Name: last_updated_on, Length: 250624, dtype: object




```python
#changes to datetime
pd.to_datetime(df['occurred_on'])
pd.to_datetime(df['created_on'])
pd.to_datetime(df['informed_on'])
pd.to_datetime(df['last_updated_on'])
```




    0        2015-09-02 06:29:16
    1        2015-09-02 06:30:19
    2        2015-09-02 08:05:39
    3        2015-09-02 07:02:01
    4        2015-09-02 07:04:25
    5        2015-09-02 07:14:33
    6        2015-09-02 07:22:39
    7        2015-09-02 07:29:44
    8        2015-09-02 07:51:02
    9        2015-09-02 07:56:00
    10       2015-09-02 08:01:24
    11       2015-09-02 08:04:17
    12       2015-09-02 08:05:40
    13       2015-09-02 08:06:23
    14       2015-09-08 07:55:15
    15       2015-09-08 07:55:28
    16       2015-09-08 07:57:17
    17       2015-09-25 08:02:53
    18       2015-09-25 08:10:23
    19       2015-09-25 06:44:22
    20       2015-09-25 08:09:50
    21       2015-09-08 08:00:48
    22       2015-09-08 08:01:48
    23       2015-09-08 08:05:37
    24       2015-09-08 08:01:54
    25       2015-09-08 08:02:21
    26       2015-09-08 08:02:28
    27       2015-09-08 08:02:44
    28       2015-09-09 06:35:12
    29       2015-09-09 06:35:41
                     ...        
    250594   1900-01-01 00:00:00
    250595   1900-01-01 00:00:00
    250596   1900-01-01 00:00:00
    250597   1900-01-01 00:00:00
    250598   1900-01-01 00:00:00
    250599   1900-01-01 00:00:00
    250600   1900-01-01 00:00:00
    250601   1900-01-01 00:00:00
    250602   1900-01-01 00:00:00
    250603   1900-01-01 00:00:00
    250604   1900-01-01 00:00:00
    250605   1900-01-01 00:00:00
    250606   1900-01-01 00:00:00
    250607   1900-01-01 00:00:00
    250608   1900-01-01 00:00:00
    250609   1900-01-01 00:00:00
    250610   1900-01-01 00:00:00
    250611   1900-01-01 00:00:00
    250612   1900-01-01 00:00:00
    250613   1900-01-01 00:00:00
    250614   1900-01-01 00:00:00
    250615   1900-01-01 00:00:00
    250616   1900-01-01 00:00:00
    250617   1900-01-01 00:00:00
    250618   1900-01-01 00:00:00
    250619   1900-01-01 00:00:00
    250620   2018-10-15 06:04:30
    250621   1900-01-01 00:00:00
    250622   1900-01-01 00:00:00
    250623   1900-01-01 00:00:00
    Name: last_updated_on, Length: 250624, dtype: datetime64[ns]



## References
- https://stackoverflow.com/questions/46241120/how-to-remove-non-alpha-numeric-characters-from-strings-within-a-dataframe-colum
- https://stackoverflow.com/questions/19726029/how-can-i-make-pandas-dataframe-column-headers-all-lowercase
- https://stackoverflow.com/questions/39768547/replace-whole-string-if-it-contains-substring-in-pandas
- https://stackoverflow.com/questions/26763344/convert-pandas-column-to-datetime
- https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html
- https://towardsdatascience.com/5-methods-to-remove-the-from-your-data-in-python-and-the-fastest-one-281489382455
- https://www.schoolbusinfo.com/faq.asp
- https://stackoverflow.com/questions/14924820/return-outside-function-error-in-python
- https://stackoverflow.com/questions/26666919/python-pandas-add-column-in-dataframe-from-list/38490727
- https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.tolist.html
- https://stackoverflow.com/questions/45264141/convert-array-into-dataframe-in-python
- 
