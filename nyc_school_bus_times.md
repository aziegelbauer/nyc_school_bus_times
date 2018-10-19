

```python
#imports libraries and csv file
import pandas as pd
df = pd.read_csv('bus-breakdown-and-delays.csv')
pd.set_option('display.max_rows', 5000)
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
#replaces characters
df['how_long_delayed'] = df['how_long_delayed'].str.replace('/', '-')
#eliminates unnecessary characters
df.how_long_delayed = df.how_long_delayed.str.replace('[a-zA-Z]', '')
```

## References
- https://stackoverflow.com/questions/46241120/how-to-remove-non-alpha-numeric-characters-from-strings-within-a-dataframe-colum
- https://stackoverflow.com/questions/19726029/how-can-i-make-pandas-dataframe-column-headers-all-lowercase
- https://stackoverflow.com/questions/39768547/replace-whole-string-if-it-contains-substring-in-pandas
