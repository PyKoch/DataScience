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

### Reading and writing files
#### csv
```python
# df stands for dataframe
# Read a csv file:
df = pd.read_csv('path_to_csv_file')

# Read a csv file that uses tabs as separators (instead of the standard comma): 
df = pd.read_csv('path_to_csv_file', sep ='\t')

# Write the dataframe to a csv file:
df.to_csv('path_to_csv_file')

# Standard export (drops the row index):
df.to_csv('output.csv', index=False)

# Use the tab or semicolon as separator instead of the comma: sep='\t' or sep=';'
df.to_csv('output.csv', index=False, sep='\t')
```
#### json
```python
df = pd.read_json('path_to_json_file')
```

### Viewing dataframe content
```python
# output the first 5 lines of the dataframe
print(df.head())

# view the first 10 lines
print(df.head(10))

# output the last 5 lines of the dataframe
print (df.tail())

# get information on the content and the type of data:
print(df.info())
```

### Operations on column content
#### splitting content into several columns
```python
# split the column with the header 'timestamp;value' into two columns called 'timestamp' and 'level'.
# You need to specify where to split (here you use the semicolon to split)
df[['timestamp', 'level']] = df['timestamp;value'].str.split(';', expand=True)
```
Here the dataframe contains the following information: 
```csv
Date and time	water level
12/30/1909, 4:00:00 Uhr	557 cm
```
The first column contains this data: "12/30/1909, 4:00:00 Uhr"
If we are only interested in the date, we can split the content by comma and take the first part (str[0])
To specify in which format the date is saved, the format = '%m/%d/%Y' makes clear that it's month, day and year, separated by '/'. 
Create a new column with just the date now as a datetime object rather than as a string: 

```python
df['Date'] = pd.to_datetime(df['Datum und Uhrzeit'].str.split(',').str[0], format='%m/%d/%Y')
```

#### delete a column
```python
# delete the column named 'length'
df = df.drop(columns=["length"])
```

#### turn time related information into date-time objects
```python
# Ensure the timestamp column is parsed as timezone-aware datetime objects
df["timestamp"] = pd.to_datetime(df["timestamp"])

# Dataframes have an index column. You can use the datetime information instead:
# (Optional) Set timestamp as index for time-series operations
df.set_index("timestamp", inplace=True)


```
### Graphing
Remember to import matplotlib (after installing it)
```python
import matplotlib.pyplot as plt
```

After your data processing you can choose between different types of plots: 

[This pdf](https://images.datacamp.com/image/upload/v1676302204/Marketing/Blog/Pandas_Cheat_Sheet.pdf) by datacamp is a good summary of the commands we will be using. 
Download it and try it out.  
