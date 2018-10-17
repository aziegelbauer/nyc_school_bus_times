

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
df['how_long_delayed'] = df['how_long_delayed'].str.replace(' ', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace(':', '')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('to', '-')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('60s', '1')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hoiur', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('one hour', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('hour', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hr', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45-1hour', '45-60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1.5hour', '90')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1.5hrs', '90')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('maybe 1/2', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('halfhour', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2hr', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1/2hour', '30')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45min-1 h', '45-60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hour15m', '75')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hr', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hour', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hours', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2hrs', '120')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('1hour', '60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('45min/60', '45-60')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('tbd', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('60-11/2 ', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('30min9', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('6030mi', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('6015', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('6015mins', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('6015m', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('60/6030 ', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('0000', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('000', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('ni0627', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('2/7/17', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('NaNn', 'NaN')
df['how_long_delayed'] = df['how_long_delayed'].str.replace('nann', 'NaN')
#df.loc[df['how_long_delayed'].str.contains('?'), 'how_long_delayed'] = 'NaN'
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
