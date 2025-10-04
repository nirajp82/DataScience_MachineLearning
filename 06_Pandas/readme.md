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

---

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

| Action             | Description                                                            | Code Example                                 | Output Type | Example Output                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------- | -------------------------------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create from list   | Create a Series from a simple Python list, with default integer index  | `pd.Series([10,20,30])`                      | Series      | <pre>0    10<br>1    20<br>2    30<br>dtype: int64</pre>                                                                                                          |
| Create with labels | Create a Series from a list but give custom index labels               | `pd.Series([10,20,30], index=['A','B','C'])` | Series      | <pre>A    10<br>B    20<br>C    30<br>dtype: int64</pre>                                                                                                          |
| Create from dict   | Construct a Series from a dict (keys become index, values become data) | `pd.Series({'A':10,'B':20,'C':30})`          | Series      | <pre>A    10<br>B    20<br>C    30<br>dtype: int64</pre>                                                                                                          |
| Boolean filter     | Filter elements of the Series by a Boolean condition                   | `s[s>15]`                                    | Series      | <pre>B    20<br>C    30<br>dtype: int64</pre>                                                                                                                     |
| Vectorized ops     | Operate elementwise with alignment by index                            | `s + pd.Series({'A':1,'C':99})`              | Series      | <pre>A     11.0<br>B      NaN<br>C    129.0<br>dtype: float64</pre>                                                                                               |
| Summary stats      | Compute descriptive statistics for numeric data                        | `s.describe()`                               | Series      | <pre>count     3.0<br>mean     20.0<br>std      10.0<br>min      10.0<br>25%      15.0<br>50%      20.0<br>75%      25.0<br>max      30.0<br>dtype: float64</pre> |

---

⚡ **Important Notes**

* A Series is like a 1D array with labels (index).
* Operations align by index (not just by position).
* Watch out for `NaN` when performing arithmetic with mismatched indices.

---

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

| Action                  | Description                                                  | Code Example                          | Output Type | Example Output                                                                                                                                                                                                                                                                                   |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Create from dict        | Build a DataFrame from a dict mapping column names to lists  | `pd.DataFrame({'A':[1,2],'B':[3,4]})` | DataFrame   | <pre>   A  B<br>0  1  3<br>1  2  4</pre>                                                                                                                                                                                                                                                         |
| Select column           | Access a single column (returns a Series)                    | `df['A']`                             | Series      | <pre>0    1<br>1    2<br>Name: A, dtype: int64</pre>                                                                                                                                                                                                                                             |
| Select multiple columns | Subset columns to produce a smaller DataFrame                | `df[['A','B']]`                       | DataFrame   | <pre>   A  B<br>0  1  3<br>1  2  4</pre>                                                                                                                                                                                                                                                         |
| Head & Tail             | Preview the first or last rows                               | `df.head()` / `df.tail()`             | DataFrame   | <pre>   A  B<br>0  1  3<br>1  2  4</pre>                                                                                                                                                                                                                                                         |
| Info                    | Show summary of DataFrame structure, non-null counts, dtypes | `df.info()`                           | Summary     | <pre><class 'pandas.core.frame.DataFrame'><br>RangeIndex: 2 entries, 0 to 1<br>Data columns (total 2 columns):<br> #   Column  Non-Null Count  Dtype<br>---  ------  --------------  -----<br> 0   A       2 non-null      int64<br> 1   B       2 non-null      int64<br>dtypes: int64(2)</pre> |
| Describe                | Compute descriptive statistics for numeric columns           | `df.describe()`                       | DataFrame   | <pre>         A    B<br>count  2.0  2.0<br>mean   1.5  3.5<br>std    0.7  0.7<br>min    1.0  3.0<br>25%    1.2  3.2<br>50%    1.5  3.5<br>75%    1.7  3.7<br>max    2.0  4.0</pre>                                                                                                               |

---

⚡ **Important Notes**

* DataFrames are 2D labeled structures with rows and columns.
* Columns are Series objects.
* Index alignment works across both rows and columns.

---

## 🟢 Indexing & Selection

| **Action**         | **Description**                                           | **Code Example**             | **Output Type** | **Example Output**                                                            |
| ------------------ | --------------------------------------------------------- | ---------------------------- | --------------- | ----------------------------------------------------------------------------- |
| Select by label    | Use `.loc[row_label, column_label]` to fetch value(s)     | `emp_df.loc[0, 'Name']`      | Scalar          | `'Alice'`                                                                     |
| Select by position | Use `.iloc[row_index, col_index]` for positional indexing | `emp_df.iloc[1, 2]`          | Scalar          | `'Los Angeles'`                                                               |
| Slice rows         | Use slicing like Python to select a range of rows         | `emp_df[0:2]`                | DataFrame       | `Name  Age         City`<br>0 Alice 25 New York<br>1 Bob 30 Los Angeles       |
| Conditional select | Filter rows based on condition(s)                         | `emp_df[emp_df['Age'] > 25]` | DataFrame       | `Name     Age      City`<br>1 Bob     30  Los Angeles<br>2 Charlie 35 Chicago |

---

⚡ **Important Notes**

* Use `.loc[]` for label-based indexing.
* Use `.iloc[]` for integer‑position based indexing.
* Slicing retains column labels.

---

## 🟢 Boolean Filtering

| Action              | Description                                 | Code Example             | Output Type                     | Example Output                |                               |
| ------------------- | ------------------------------------------- | ------------------------ | ------------------------------- | ----------------------------- | ----------------------------- |
| Simple filter       | Filter rows where a single condition is met | `df[df['A']>1]`          | DataFrame                       | <pre>   A  B<br>1  2  4</pre> |                               |
| Multiple conditions | Combine conditions with `&`, `              | `, `~` (use parentheses) | `df[(df['A']>1) & (df['B']<5)]` | DataFrame                     | <pre>   A  B<br>1  2  4</pre> |

---

⚡ **Important Notes**

* Use bitwise operators `&`, `|`, `~` with parentheses; **don’t** use Python `and`, `or`, `not`.
* Filtering returns a new DataFrame; original remains unchanged.

---

## 🟢 Missing Data

| Action             | Description                                  | Code Example   | Output Type | Example Output                                                   |
| ------------------ | -------------------------------------------- | -------------- | ----------- | ---------------------------------------------------------------- |
| Detect missing     | Identify missing values (`NaN`) in DataFrame | `df.isnull()`  | DataFrame   | <pre>       A      B<br>0  False  False<br>1  False  False</pre> |
| Drop rows with NaN | Remove rows containing any `NaN`             | `df.dropna()`  | DataFrame   | <pre>   A  B<br>0  1  3<br>1  2  4</pre>                         |
| Fill missing       | Replace `NaN` with a specified value         | `df.fillna(0)` | DataFrame   | <pre>   A  B<br>0  1  3<br>1  2  4</pre>                         |

---

⚡ **Important Notes**

* `NaN` stands for “Not a Number” (i.e. missing).
* Dropping may cause data loss; filling is safer in many cases.
* Also consider `fillna(method='ffill', 'bfill')`, `interpolate()`, `dropna(axis=1)`, etc.

---

## 🟢 GroupBy & Aggregation

| Action          | Description                                                    | Code Example                                    | Output Type | Example Output                                                                                 |
| --------------- | -------------------------------------------------------------- | ----------------------------------------------- | ----------- | ---------------------------------------------------------------------------------------------- |
| Group by column | Group rows by a column and apply aggregation (sum, mean, etc.) | `df.groupby('col').sum()`                       | DataFrame   | <pre>col  value<br>A    10<br>B    20</pre>                                                    |
| Multiple agg    | Apply multiple aggregation functions for each group            | `df.groupby('col').agg({'val':['mean','max']})` | DataFrame   | <pre>     val       <br>    mean  max<br>col            <br>A    5.0   9<br>B   20.0  20</pre> |

---

⚡ **Important Notes**

* GroupBy = split → apply → combine.
* Aggregation functions include `sum`, `mean`, `count`, `max`, `min`, `std`, `first`, `last`.
* Use `.agg()` to combine multiple aggregation operations.

---

## 🟢 Merge & Join

| Action          | Description                                | Code Example                                | Output Type | Example Output                                                   |
| --------------- | ------------------------------------------ | ------------------------------------------- | ----------- | ---------------------------------------------------------------- |
| Merge on column | Perform SQL‑style join on common column(s) | `pd.merge(df1, df2, on='key')`              | DataFrame   | <pre>key  val1  val2<br>1    10    100<br>2    20    200</pre>   |
| Join on index   | Join DataFrames by index alignment         | `df1.join(df2, lsuffix='_L', rsuffix='_R')` | DataFrame   | <pre>     val1  val2<br>0      10   100<br>1      20   200</pre> |

---

⚡ **Important Notes**

* `pd.merge()` is analogous to SQL joins: inner / left / right / outer (specify via `how=`).
* `df.join()` is index-based and simpler for index alignment.
* Use suffixes (`lsuffix`, `rsuffix`) to avoid overlapping column names.

---

## 🟢 Reshaping

| Action | Description                                                                        | Code Example                                        | Output Type | Example Output                                                                   |
| ------ | ---------------------------------------------------------------------------------- | --------------------------------------------------- | ----------- | -------------------------------------------------------------------------------- |
| Pivot  | Turn “long” format into “wide” by using one column for new columns, one for values | `df.pivot(index='id', columns='var', values='val')` | DataFrame   | <pre>var  A  B<br>id        <br>1   10 NaN<br>2  NaN  20</pre>                   |
| Melt   | Convert “wide” formats into “long” by unpivoting                                   | `pd.melt(df, id_vars=['id'])`                       | DataFrame   | <pre>   id variable  value<br>0   1       A     10<br>1   2       B     20</pre> |

---

⚡ **Important Notes**

* Pivot = long → wide; Melt = wide → long.
* Use `stack()`, `unstack()` for multi-index reshaping.
* `pivot_table()` is a robust version of pivot with aggregation capabilities.

---

## 🟢 Time Series

| Action                | Description                                                           | Code Example                             | Output Type        | Example Output                                                                                         |
| --------------------- | --------------------------------------------------------------------- | ---------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------ |
| Create datetime index | Generate a sequence of dates/times with specified frequency           | `pd.date_range('2025-01-01', periods=3)` | DatetimeIndex      | <pre>DatetimeIndex(['2025-01-01', '2025-01-02', '2025-01-03'], dtype='datetime64[ns]', freq='D')</pre> |
| Resample              | Aggregate time-indexed data at a new frequency (e.g. daily → monthly) | `ts.resample('M').mean()`                | Series / DataFrame | <pre>2025-01-31    10.0<br>2025-02-28    20.0<br>Freq: M, dtype: float64</pre>                         |

---

⚡ **Important Notes**

* Pandas handles time series natively via `DatetimeIndex`.
* Use `resample()`, `asfreq()`, `shift()`, `rolling()`, `expanding()`, etc.
* For timezone-aware data: `tz_localize()`, `tz_convert()`, `dt` accessor for date components.

---

## 🟢 Input & Output

| Action      | Description                                            | Code Example                               | Output Type     | Example Output                               |
| ----------- | ------------------------------------------------------ | ------------------------------------------ | --------------- | -------------------------------------------- |
| CSV Read    | Read a comma-separated values file into a DataFrame    | `pd.read_csv('file.csv')`                  | DataFrame       | <pre>   A  B<br>0  1  3<br>1  2  4</pre>     |
| CSV Write   | Export a DataFrame to CSV                              | `df.to_csv('file.csv')`                    | File / Output   | *CSV file written*                           |
| Excel Read  | Read an Excel file into a DataFrame                    | `pd.read_excel('file.xlsx')`               | DataFrame       | <pre>   A  B<br>0  1  3<br>1  2  4</pre>     |
| Excel Write | Write a DataFrame to an Excel file                     | `df.to_excel('file.xlsx')`                 | File / Output   | *Excel file written*                         |
| HTML Read   | Parse HTML tables from a file or URL into DataFrame(s) | `pd.read_html('file_or_url.html')`         | List[DataFrame] | *List of DataFrames parsed from HTML tables* |
| JSON Read   | Read JSON string or file into a DataFrame              | `pd.read_json('file.json')`                | DataFrame       | *Parsed JSON → DataFrame*                    |
| JSON Write  | Export a DataFrame to JSON                             | `df.to_json('file.json')`                  | File / String   | *JSON string or file content*                |
| SQL Read    | Execute SQL query or read SQL table into DataFrame     | `pd.read_sql('SELECT * FROM table', conn)` | DataFrame       | *Query result as DataFrame*                  |

---

⚡ **Important Notes**

* Pandas supports many I/O formats: CSV, Excel, JSON, HTML, SQL, Parquet, HDF, and more.
* Always verify delimiters, encoding, missing value formats when reading text files.
* **`read_html()`** is special: it returns a **list** of DataFrames (one per HTML table found).
* For large datasets, consider using `chunksize=`, `iterator=True`, or reading in parts.
