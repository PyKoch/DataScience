# DataScience

## Pandas
Pandas is a library that allows you to handle 'dataframes' (and 'series'), which you can think of as spreadsheets. 

Install pandas on Windows: 
```
pip install pandas
```
Install pandas on Macs:
```
pip3 install pandas
```
Import pandas (usually as 'pd'):
```python
import pandas as pd
```

### Reading files
#### csv
```python
df = pd.read_csv(path_to_csv_file)
# df stands for dataframe
```

### Viewing dataframe content
```python
# oiutput the first 5 lines of the dataframe
print(df.head())  

# output the last 5 lines of the dataframe
print (df.tail())
```
### Operations on column content
#### splitting content into several columns
```python
# split the column with the header 'timestamp;value' into two columns called 'timestamp' and 'level':
df[['timestamp', 'level']] = df['timestamp;value'].str.split(';', expand=True)
```

#### delete a column
```python
# delete the column named 'length'
df = df.drop(columns=["length"])
```

[This pdf](https://images.datacamp.com/image/upload/v1676302204/Marketing/Blog/Pandas_Cheat_Sheet.pdf) by datacamp is a good summary of the commands we will be using. 
Download it and try it out.  
