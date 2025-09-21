# 📊 Pandas Quick Reference Cheatsheet

## 📑 Table of Contents

1. [Pandas Series](#pandas-series)
2. [DataFrames](#dataframes)
3. [Indexing & Selection](#indexing--selection)
4. [Boolean Filtering](#boolean-filtering)
5. [Missing Data](#missing-data)
6. [GroupBy & Aggregation](#groupby--aggregation)
7. [Merge & Join](#merge--join)
8. [Reshaping](#reshaping)
9. [Time Series](#time-series)
10. [Input & Output](#input--output)

------------------------------------------------------------------------

## 🟢 Pandas Series

```python
import pandas as pd

s = pd.Series([10, 20, 30], index=['A', 'B', 'C'])
print(s)
```

**Output:**

```text
A    10
B    20
C    30
dtype: int64
```

### Quick Reference --- Pandas Series

| Action       | Code Example                                 | Output Type | Example Output |
|--------------|----------------------------------------------|-------------|----------------|
| Create from list | `pd.Series([10,20,30])` | Series | ```text
0    10
1    20
2    30
dtype: int64
``` |
| Create with labels | `pd.Series([10,20,30], index=['A','B','C'])` | Series | ```text
A    10
B    20
C    30
dtype: int64
``` |
| Create from dict | `pd.Series({'A':10,'B':20,'C':30})` | Series | ```text
A    10
B    20
C    30
dtype: int64
``` |
| Boolean filter | `s[s>15]` | Series | ```text
B    20
C    30
dtype: int64
``` |
| Vectorized ops | `s + pd.Series({'A':1,'C':99})` | Series | ```text
A     11.0
B      NaN
C    129.0
dtype: float64
``` |
| Summary stats | `s.describe()` | Series | ```text
count     3.0
mean     20.0
std      10.0
min      10.0
25%      15.0
50%      20.0
75%      25.0
max      30.0
dtype: float64
``` |

------------------------------------------------------------------------

⚡ **Important Notes**  
- A Series is like a 1D array with labels (index).  
- Operations align by index (not just position).  
- Watch out for `NaN` when doing arithmetic with mismatched indices.  

------------------------------------------------------------------------

## 🟢 DataFrames

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}
emp_df = pd.DataFrame(data)
print(emp_df)
```

**Output:**

```text
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

### Quick Reference --- DataFrame

| Action       | Code Example | Output Type | Example Output |
|--------------|--------------|-------------|----------------|
| Select single column | `emp_df['Name']` | Series | ```text
0      Alice
1        Bob
2    Charlie
Name: Name, dtype: object
``` |
| Select multiple columns | `emp_df[['Name','Age']]` | DataFrame | ```text
      Name  Age
0    Alice   25
1      Bob   30
2  Charlie   35
``` |
| Add new column | `emp_df['Age+5'] = emp_df['Age'] + 5` | DataFrame | Adds a new column |
| Drop column | `emp_df.drop('City', axis=1)` | DataFrame | Removes "City" column |
| Drop row | `emp_df.drop(1, axis=0)` | DataFrame | Removes Bob's row |
| Shape | `emp_df.shape` | tuple | ```text
(3, 3)
``` |
| Select row by label | `emp_df.loc[0]` | Series | Alice row |
| Select row by position | `emp_df.iloc[2]` | Series | Charlie row |

------------------------------------------------------------------------

⚡ **Important Notes**  
- A DataFrame is a 2D table of rows and columns (like Excel).  
- Columns are `Series` inside the DataFrame.  
- `.loc` = label-based indexing, `.iloc` = position-based indexing.  

------------------------------------------------------------------------

## 🟢 Indexing & Selection

```python
print(emp_df.loc[0, 'Name'])
print(emp_df.iloc[1, 1])
```

**Output:**

```text
Alice
30
```

### Quick Reference --- Indexing

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Select cell by label | `emp_df.loc[0,'Name']` | ```text
Alice
``` |
| Select cell by position | `emp_df.iloc[1,1]` | ```text
30
``` |
| Select row range | `emp_df[0:2]` | ```text
     Name  Age         City
0  Alice   25     New York
1    Bob   30  Los Angeles
``` |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Use `.loc` for labels, `.iloc` for integer positions.  
- Slicing rows with `:` works like NumPy.  

------------------------------------------------------------------------

## 🟢 Boolean Filtering

```python
print(emp_df[emp_df['Age'] > 25])
```

**Output:**

```text
      Name  Age      City
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

### Quick Reference --- Boolean Filtering

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Filter rows | `emp_df[emp_df['Age']>25]` | ```text
      Name  Age      City
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
``` |
| Multiple conditions | `emp_df[(emp_df['Age']>25) & (emp_df['City']=='Chicago')]` | Filters only matching rows |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Conditions must be wrapped in parentheses.  
- Use `&` for AND, `|` for OR.  

------------------------------------------------------------------------

## 🟢 Missing Data

```python
df = pd.DataFrame({
    'A':[1,2,None],
    'B':[None,5,6]
})
print(df)
```

**Output:**

```text
     A    B
0  1.0  NaN
1  2.0  5.0
2  NaN  6.0
```

### Quick Reference --- Missing Data

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Drop rows with NaN | `df.dropna()` | Removes row with NaN |
| Fill missing values | `df.fillna(0)` | ```text
     A    B
0  1.0  0.0
1  2.0  5.0
2  0.0  6.0
``` |
| Check nulls | `df.isnull()` | Boolean mask |
| Drop cols if all NaN | `df.dropna(axis=1, how='all')` | Removes empty columns |

------------------------------------------------------------------------

⚡ **Important Notes**  
- `NaN` is treated as float.  
- Always handle missing values before analysis.  

------------------------------------------------------------------------

## 🟢 GroupBy & Aggregation

```python
sales = pd.DataFrame({
    'Category':['Fruit','Fruit','Veg','Veg'],
    'Amount':[10,20,15,25]
})
print(sales.groupby('Category').sum())
```

**Output:**

```text
          Amount
Category        
Fruit         30
Veg           40
```

### Quick Reference --- GroupBy

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Group by col and sum | `sales.groupby('Category').sum()` | ```text
          Amount
Category        
Fruit         30
Veg           40
``` |
| Multiple aggs | `sales.groupby('Category').agg(['sum','mean'])` | Computes multiple aggregates |
| Group and count | `sales.groupby('Category').count()` | Counts rows per group |

------------------------------------------------------------------------

⚡ **Important Notes**  
- GroupBy splits data → apply function → combine results.  
- Supports multiple aggregates via `.agg()`.  

------------------------------------------------------------------------

## 🟢 Merge & Join

```python
left = pd.DataFrame({'ID':[1,2], 'Name':['Alice','Bob']})
right = pd.DataFrame({'ID':[1,2], 'Score':[85,90]})
print(pd.merge(left,right,on='ID'))
```

**Output:**

```text
   ID   Name  Score
0   1  Alice     85
1   2    Bob     90
```

### Quick Reference --- Merge & Join

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Inner join | `pd.merge(left,right,on='ID')` | Merges only matching keys |
| Left join | `pd.merge(left,right,on='ID',how='left')` | Keeps all left rows |
| Right join | `pd.merge(left,right,on='ID',how='right')` | Keeps all right rows |
| Outer join | `pd.merge(left,right,on='ID',how='outer')` | Keeps all rows |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Default join type is `inner`.  
- Use `how` argument to control join type.  

------------------------------------------------------------------------

## 🟢 Reshaping

```python
df = pd.DataFrame({
    'Name':['Alice','Bob'],
    'Subject':['Math','Math'],
    'Score':[90,85]
})
pivoted = df.pivot(index='Name', columns='Subject', values='Score')
print(pivoted)
```

**Output:**

```text
Subject  Math
Name          
Alice       90
Bob         85
```

### Quick Reference --- Reshaping

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Pivot table | `df.pivot(index='Name',columns='Subject',values='Score')` | Reshapes data |
| Melt | `pd.melt(pivoted.reset_index(),id_vars='Name')` | Unpivots back |
| Stack | `pivoted.stack()` | Converts cols to rows |
| Unstack | `pivoted.stack().unstack()` | Converts rows back to cols |

------------------------------------------------------------------------

⚡ **Important Notes**  
- `pivot` reshapes long → wide.  
- `melt` reshapes wide → long.  

------------------------------------------------------------------------

## 🟢 Time Series

```python
dates = pd.date_range('2023-01-01', periods=3)
ts = pd.Series([100,200,300], index=dates)
print(ts)
```

**Output:**

```text
2023-01-01    100
2023-01-02    200
2023-01-03    300
Freq: D, dtype: int64
```

### Quick Reference --- Time Series

| Action       | Code Example | Example Output |
|--------------|--------------|----------------|
| Date range | `pd.date_range('2023-01-01',periods=3)` | ```text
DatetimeIndex(['2023-01-01','2023-01-02','2023-01-03'],dtype='datetime64[ns]',freq='D')
``` |
| Shift | `ts.shift(1)` | Shifts values |
| Resample | `ts.resample('M').sum()` | Monthly sum |
| Rolling mean | `ts.rolling(2).mean()` | Windowed mean |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Pandas has built-in date/time handling.  
- Use `resample` for time-based grouping.  

------------------------------------------------------------------------

## 🟢 Input & Output

```python
# CSV
emp_df.to_csv('data.csv', index=False)
df2 = pd.read_csv('data.csv')
print(df2)
```

**Output (CSV saved and read back):**

```text
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

### Quick Reference --- I/O

| Action       | Code Example |
|--------------|--------------|
| Read CSV | `pd.read_csv('file.csv')` |
| Write CSV | `df.to_csv('file.csv', index=False)` |
| Read Excel | `pd.read_excel('file.xlsx')` |
| Write Excel | `df.to_excel('file.xlsx', index=False)` |
| Read SQL | `pd.read_sql(query, conn)` |
| Read JSON | `pd.read_json('file.json')` |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Pandas supports many formats (CSV, Excel, SQL, JSON).  
- Always check encoding when reading external files.  

------------------------------------------------------------------------
