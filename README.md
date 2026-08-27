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
Saving it all in a new column 'Date':

```python
df['Date'] = df['Datum und Uhrzeit'].str.split(',').str[0]
```

#### delete a column
```python
# delete the column named 'length'
df = df.drop(columns=["length"])
```

#### turn time related information into date-time objects
If the 'Date' column contains 
```csv
12/21/2026
```
as a string, then this date can be converted to a datetime object (for easier processing):

```python
# Ensure the timestamp column is parsed as timezone-aware datetime objects
# %m: month, 1 or 2 digits, %d: day of the month, 1 or 2 digits, %Y: 4 digit year
df["Date"] = pd.to_datetime(df["Date"], format = '%m/%d/%Y')

# Then you can extract day, month or year with this command: 
```python
df['Month'] = df['Date'].dt.month
```
Dataframes have an index column. You can use the datetime information instead:
```python
# (Optional) Set timestamp as index for time-series operations
df.set_index("timestamp", inplace=True)
```
#### grouping and calculations
Grouping allows you to arrange your data based on the column you choose:
```python
df = df.groupby('Month')
```
Calculate the mean for each month: 
```python
df_mean = df.groupby('Month')['value'].mean()
```

### Graphing
Remember to import matplotlib (after installing it)
```python
import matplotlib.pyplot as plt
```

After your data processing you can choose between different types of plots: 

### User picking files and interacting
The 'askopenfilename()' function allows the user to pick a file during the execution of the code. When you want to use various files, this can be handy. 
```python
from tkinter import filedialog

path = filedialog.askopenfilename()

# You can even give a prompt what the user should do:
path = filedialog.askopenfilename(title="Select Historical Water Level CSV")

# You can specify which file types can be picked (to avoid mistakes)
path = filedialog.askopenfilename(filetypes=[("CSV files", "*.csv")])

# You can specify the directory which will be opened
path = filedialog.askopenfilename(initialdir = '/Users/vk0604/Documents/Coding')
```
[This pdf](https://images.datacamp.com/image/upload/v1676302204/Marketing/Blog/Pandas_Cheat_Sheet.pdf) by datacamp is a good summary of the commands we will be using. 
Download it and try it out.  
