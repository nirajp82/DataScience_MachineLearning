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

### Quick Reference — Pandas Series

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Create from list | `pd.Series([10,20,30])` | Series | <pre>0    10<br>1    20<br>2    30<br>dtype: int64</pre> |
| Create with labels | `pd.Series([10,20,30], index=['A','B','C'])` | Series | <pre>A    10<br>B    20<br>C    30<br>dtype: int64</pre> |
| Create from dict | `pd.Series({'A':10,'B':20,'C':30})` | Series | <pre>A    10<br>B    20<br>C    30<br>dtype: int64</pre> |
| Boolean filter | `s[s>15]` | Series | <pre>B    20<br>C    30<br>dtype: int64</pre> |
| Vectorized ops | `s + pd.Series({'A':1,'C':99})` | Series | <pre>A     11.0<br>B      NaN<br>C    129.0<br>dtype: float64</pre> |
| Summary stats | `s.describe()` | Series | <pre>count     3.0<br>mean     20.0<br>std      10.0<br>min      10.0<br>25%      15.0<br>50%      20.0<br>75%      25.0<br>max      30.0<br>dtype: float64</pre> |

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

### Quick Reference — DataFrames

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Create from dict | `pd.DataFrame({'A':[1,2],'B':[3,4]})` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Select column | `df['A']` | Series | <pre>0    1<br>1    2<br>Name: A, dtype: int64</pre> |
| Select multiple columns | `df[['A','B']]` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Head & Tail | `df.head()` / `df.tail()` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Info | `df.info()` | Summary | <pre><class 'pandas.core.frame.DataFrame'><br>RangeIndex: 2 entries, 0 to 1<br>Data columns (total 2 columns):<br> #   Column  Non-Null Count  Dtype<br>---  ------  --------------  -----<br> 0   A       2 non-null      int64<br> 1   B       2 non-null      int64<br>dtypes: int64(2)</pre> |
| Describe | `df.describe()` | DataFrame | <pre>         A    B<br>count  2.0  2.0<br>mean   1.5  3.5<br>std    0.7  0.7<br>min    1.0  3.0<br>25%    1.2  3.2<br>50%    1.5  3.5<br>75%    1.7  3.7<br>max    2.0  4.0</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- DataFrames are 2D labeled structures with rows and columns.  
- Columns are `Series` objects.  
- Index alignment works across rows and columns.  

------------------------------------------------------------------------

## 🟢 Indexing & Selection

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Select by label | `df.loc[0,'A']` | Scalar | <pre>1</pre> |
| Select by position | `df.iloc[0,0]` | Scalar | <pre>1</pre> |
| Slice rows | `df[0:2]` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Conditional select | `df[df['A']>1]` | DataFrame | <pre>   A  B<br>1  2  4</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Use `.loc[]` for label-based indexing.  
- Use `.iloc[]` for integer position indexing.  
- Slicing preserves column labels.  

------------------------------------------------------------------------

## 🟢 Boolean Filtering

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Simple filter | `df[df['A']>1]` | DataFrame | <pre>   A  B<br>1  2  4</pre> |
| Multiple conditions | `df[(df['A']>1) & (df['B']<5)]` | DataFrame | <pre>   A  B<br>1  2  4</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Use `&` (AND), `|` (OR), `~` (NOT) with parentheses.  
- Filtering returns a new DataFrame, index preserved.  

------------------------------------------------------------------------

## 🟢 Missing Data

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Detect missing | `df.isnull()` | DataFrame | <pre>       A      B<br>0  False  False<br>1  False  False</pre> |
| Drop rows with NaN | `df.dropna()` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Fill missing | `df.fillna(0)` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- `NaN` stands for Not a Number (missing values).  
- Dropping may lose data, filling replaces intelligently.  

------------------------------------------------------------------------

## 🟢 GroupBy & Aggregation

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Group by column | `df.groupby('col').sum()` | DataFrame | <pre>col  value<br>A    10<br>B    20</pre> |
| Multiple agg | `df.groupby('col').agg({'val':['mean','max']})` | DataFrame | <pre>     val       <br>    mean  max<br>col            <br>A    5.0   9<br>B   20.0  20</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- GroupBy = Split → Apply → Combine.  
- Aggregations: `sum`, `mean`, `count`, `max`, etc.  
- Use `.agg()` for multiple functions at once.  

------------------------------------------------------------------------

## 🟢 Merge & Join

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Merge on column | `pd.merge(df1, df2, on='key')` | DataFrame | <pre>key  val1  val2<br>1    10    100<br>2    20    200</pre> |
| Join on index | `df1.join(df2, lsuffix='_L', rsuffix='_R')` | DataFrame | <pre>     val1  val2<br>0      10   100<br>1      20   200</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- `merge` works like SQL joins.  
- Types: inner, left, right, outer.  
- `join` works on index alignment.  

------------------------------------------------------------------------

## 🟢 Reshaping

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Pivot | `df.pivot(index='id', columns='var', values='val')` | DataFrame | <pre>var  A  B<br>id        <br>1   10 NaN<br>2  NaN  20</pre> |
| Melt | `pd.melt(df, id_vars=['id'])` | DataFrame | <pre>   id variable  value<br>0   1       A     10<br>1   2       B     20</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Pivot: long → wide format.  
- Melt: wide → long format.  
- Use `stack`/`unstack` for hierarchical reshaping.  

------------------------------------------------------------------------

## 🟢 Time Series

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| Create datetime index | `pd.date_range('2025-01-01', periods=3)` | DatetimeIndex | <pre>DatetimeIndex(['2025-01-01', '2025-01-02', '2025-01-03'], dtype='datetime64[ns]', freq='D')</pre> |
| Resample | `ts.resample('M').mean()` | Series | <pre>2025-01-31    10.0<br>2025-02-28    20.0<br>Freq: M, dtype: float64</pre> |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Pandas handles time series natively with `DatetimeIndex`.  
- Resampling useful for aggregating (daily → monthly).  

------------------------------------------------------------------------

## 🟢 Input & Output

| Action | Code Example | Output Type | Example Output |
|--------|--------------|-------------|----------------|
| CSV Read | `pd.read_csv('file.csv')` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| CSV Write | `df.to_csv('file.csv')` | File | *CSV file written* |
| Excel Read | `pd.read_excel('file.xlsx')` | DataFrame | <pre>   A  B<br>0  1  3<br>1  2  4</pre> |
| Excel Write | `df.to_excel('file.xlsx')` | File | *Excel file written* |

------------------------------------------------------------------------

⚡ **Important Notes**  
- Pandas supports CSV, Excel, JSON, SQL, Parquet, etc.  
- Always check separators and encoding when reading text files.  
