# 📊 Pandas Quick Reference Cheatsheet
---

## 🟢 Section 1: Pandas Series

```python
import pandas as pd

s = pd.Series([10, 20, 30], index=['A', 'B', 'C'])
print(s)
```

**Output:**

```
A    10
B    20
C    30
dtype: int64
```

### Quick Reference — Pandas Series

| Action                           | Code Example                                 | Output Type | Example Output                                                                                  |
| -------------------------------- | -------------------------------------------- | ----------- | ----------------------------------------------------------------------------------------------- |
| Create from list                 | `pd.Series([10,20,30])`                      | Series      | `\n0    10\n1    20\n2    30\ndtype: int64\n`                                                   |
| Create with labels               | `pd.Series([10,20,30], index=['A','B','C'])` | Series      | `\nA    10\nB    20\nC    30\ndtype: int64\n`                                                   |
| Create from dict                 | `pd.Series({'A':10,'B':20,'C':30})`          | Series      | `\nA    10\nB    20\nC    30\ndtype: int64\n`                                                   |
| Access by label                  | `s['A']`                                     | Scalar      | `10`                                                                                            |
| Access by position               | `s[0]` or `s.iloc[0]`                        | Scalar      | `10`                                                                                            |
| Slice by label                   | `s['A':'B']`                                 | Series      | `\nA    10\nB    20\ndtype: int64\n`                                                            |
| Boolean filter                   | `s[s>15]`                                    | Series      | `\nB    20\nC    30\ndtype: int64\n`                                                            |
| Vectorized ops (aligns by index) | `s + pd.Series({'A':1,'C':99})`              | Series      | `\nA     11.0\nB      NaN\nC    129.0\ndtype: float64\n`                                        |
| Inspect values                   | `s.values`                                   | ndarray     | `[10 20 30]`                                                                                    |
| Inspect index                    | `s.index`                                    | Index       | `Index(['A','B','C'], dtype='object')`                                                          |
| Check dtype                      | `s.dtype`                                    | dtype       | `int64`                                                                                         |
| Count elements                   | `s.size`                                     | int         | `3`                                                                                             |
| Handle missing (fill)            | `s.fillna(0)`                                | Series      | fills NaN with 0                                                                                |
| Drop missing                     | `s.dropna()`                                 | Series      | removes NaN rows                                                                                |
| Reindex                          | `s.reindex(['A','B','C','D'])`               | Series      | `\nA    10.0\nB    20.0\nC    30.0\nD     NaN\ndtype: float64\n`                                |
| Summary stats                    | `s.describe()`                               | Series      | `\ncount     3.0\nmean     20.0\nstd      10.0\nmin      10.0\nmax      30.0\ndtype: float64\n` |
| Value counts                     | `s.value_counts()`                           | Series      | `\n10    1\n20    1\n30    1\ndtype: int64\n`                                                   |
| Sort by index                    | `s.sort_index()`                             | Series      | sorted by labels                                                                                |
| Sort by values                   | `s.sort_values()`                            | Series      | sorted numerically                                                                              |
| Convert dtype                    | `s.astype(float)`                            | Series      | `\nA    10.0\nB    20.0\nC    30.0\ndtype: float64\n`                                           |
| To dict                          | `s.to_dict()`                                | dict        | `{'A':10,'B':20,'C':30}`                                                                        |
| Unique values                    | `s.unique()`                                 | ndarray     | `[10 20 30]`                                                                                    |
| Number unique                    | `s.nunique()`                                | int         | `3`                                                                                             |
| Head / Tail                      | `s.head(2) / s.tail(2)`                      | Series      | `\nA    10\nB    20\ndtype: int64\n` (head)<br>` \nB    20\nC    30\ndtype: int64\n` (tail)     |

---

## 🟢 Section 2: DataFrame Basics

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

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

### Quick Reference — DataFrame

| Action                    | Code Example                         | Output Type | Example Output                                                                   |
| ------------------------- | ------------------------------------ | ----------- | -------------------------------------------------------------------------------- |
| Select single column      | `emp_df['Name']`                     | Series      | `\n0      Alice\n1        Bob\n2    Charlie\nName: Name, dtype: object\n`        |
| Select multiple columns   | `emp_df[['Name','Age']]`             | DataFrame   | `\n      Name  Age\n0    Alice   25\n1      Bob   30\n2  Charlie   35\n`         |
| Check type of selection   | `type(emp_df['Name'])`               | Series      | `<class 'pandas.core.series.Series'>`                                            |
| Add new column            | `emp_df['New'] = emp_df['Age'] + 5`  | DataFrame   | Adds "New" column with values `[30, 35, 40]`                                     |
| Drop column (not inplace) | `emp_df.drop('New', axis=1)`         | DataFrame   | Returns DataFrame without "New"                                                  |
| Drop row                  | `emp_df.drop(1, axis=0)`             | DataFrame   | Removes Bob’s row                                                                |
| Shape of DataFrame        | `emp_df.shape`                       | Tuple       | `(3, 3)`                                                                         |
| Select row by label       | `emp_df.loc[0]`                      | Series      | `\nName     Alice\nAge         25\nCity    New York\nName: 0, dtype: object\n`   |
| Select row by position    | `emp_df.iloc[2]`                     | Series      | `\nName    Charlie\nAge          35\nCity     Chicago\nName: 2, dtype: object\n` |
| Subset rows/columns       | `emp_df.loc[[0,2], ['Name','City']]` | DataFrame   | `\n      Name      City\n0    Alice  New York\n2  Charlie   Chicago\n`           |

---

## 🟢 Section 3: Boolean Filtering

| Action                 | Code Example                                                 | Output Type                       | Example Output                                              |                     |
| ---------------------- | ------------------------------------------------------------ | --------------------------------- | ----------------------------------------------------------- | ------------------- |
| Boolean mask           | `emp_df > 25`                                                | DataFrame                         | Shows `True/False` per cell                                 |                     |
| Conditional selection  | `emp_df[emp_df['Age'] > 25]`                                 | DataFrame                         | Bob & Charlie rows                                          |                     |
| Multiple conditions    | `emp_df[(emp_df['Age'] > 25) & (emp_df['City']=="Chicago")]` | DataFrame                         | Charlie only                                                |                     |
| OR condition           | \`emp\_df\[(emp\_df\['Age'] > 25)                            | (emp\_df\['City']=="New York")]\` | DataFrame                                                   | Alice, Bob, Charlie |
| Filter + select column | `emp_df[emp_df['Age'] > 25]['Name']`                         | Series                            | `\n1        Bob\n2    Charlie\nName: Name, dtype: object\n` |                     |
| Reset index            | `emp_df.reset_index()`                                       | DataFrame                         | resets index                                                |                     |

---

## 🟢 Section 4: MultiIndex DataFrame

```python
arrays = [
    ['New York','New York','New York','Los Angeles','Los Angeles','Chicago','Chicago'],
    ['Alice','Bob','Bob','Charlie','David','Eva','Frank']
]
index = pd.MultiIndex.from_arrays(arrays, names=('City','Name'))

emp_df_multi = pd.DataFrame({
    'Age': [25, 30, 31, 35, 28, 40, 32],
    'Score': [88, 92, 85, 79, 85, 95, 90]
}, index=index)

print(emp_df_multi)
```

**Output:**

```
                   Age  Score
City        Name
New York    Alice    25     88
            Bob      30     92
            Bob      31     85
Los Angeles Charlie  35     79
            David    28     85
Chicago     Eva      40     95
            Frank    32     90
```

### Quick Reference — MultiIndex

| Action             | Code Example                                               | Output Type | Example Output                                          |
| ------------------ | ---------------------------------------------------------- | ----------- | ------------------------------------------------------- |
| Create multi-index | `pd.MultiIndex.from_arrays(arrays, names=('City','Name'))` | MultiIndex  | `[('New York','Alice'), ...]`                           |
| Access outer index | `emp_df_multi.loc['New York']`                             | DataFrame   | Alice & Bob rows                                        |
| Access inner index | `emp_df_multi.loc['Chicago'].loc['Eva']`                   | Series      | `\nAge      40\nScore    95\nName: Eva, dtype: int64\n` |
| Cross-section      | `emp_df_multi.xs('Bob', level='Name')`                     | DataFrame   | rows where Name = Bob                                   |

---

## 🟢 Section 5: Missing Data

```python
import numpy as np
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [25, np.nan, 30, np.nan, 40],
    'City': ['New York', 'Los Angeles', np.nan, 'Chicago', 'Chicago']
}
df = pd.DataFrame(data)
print(df)
```

**Output:**

```
      Name   Age         City
0    Alice  25.0     New York
1      Bob   NaN  Los Angeles
2  Charlie  30.0         NaN
3    David   NaN      Chicago
4      Eva  40.0      Chicago
```

### Quick Reference — Missing Data

| Action                     | Code Example                         | Output Type | Example Output                  |
| -------------------------- | ------------------------------------ | ----------- | ------------------------------- |
| Drop rows with NaN         | `df.dropna()`                        | DataFrame   | only Alice & Eva rows           |
| Drop columns with NaN      | `df.dropna(axis=1)`                  | DataFrame   | only Name column                |
| Drop rows with ≥2 non-null | `df.dropna(thresh=2)`                | DataFrame   | keeps rows with ≥2 valid values |
| Fill missing constant      | `df.fillna('Unknown')`               | DataFrame   | replaces NaN with `'Unknown'`   |
| Fill with mean             | `df['Age'].fillna(df['Age'].mean())` | Series      | fills NaN with \~31.67          |
| Forward fill               | `df.fillna(method='ffill')`          | DataFrame   | propagates last value           |
| Backward fill              | `df.fillna(method='bfill')`          | DataFrame   | propagates next value           |

---

## 🟢 Section 6: GroupBy

```python
group_data = {
    'Company': ['Google','Google','Microsoft','Microsoft','Facebook','Facebook'],
    'Employee': ['Sam','Charlie','Amy','Vanessa','Carl','Sarah'],
    'Sales': [200,120,340,124,243,350]
}
df = pd.DataFrame(group_data)
print(df)
```

**Output:**

```
     Company Employee  Sales
0     Google      Sam    200
1     Google  Charlie    120
2  Microsoft      Amy    340
3  Microsoft  Vanessa    124
4   Facebook     Carl    243
5   Facebook    Sarah    350
```

### Quick Reference — GroupBy

| Action                | Code Example                                  | Output Type | Example Output            |
| --------------------- | --------------------------------------------- | ----------- | ------------------------- |
| Create GroupBy object | `df.groupby('Company')`                       | GroupBy     | GroupBy object            |
| Mean of groups        | `df.groupby('Company').mean()`                | DataFrame   | average sales per company |
| Sum of groups         | `df.groupby('Company').sum()`                 | DataFrame   | total sales per company   |
| Std deviation         | `df.groupby('Company').std()`                 | DataFrame   | spread of sales           |
| Count values          | `df.groupby('Company').count()`               | DataFrame   | counts per company        |
| Min / Max values      | `df.groupby('Company').min()`                 | DataFrame   | minimum per company       |
| Access single group   | `df.groupby('Company').sum().loc['Facebook']` | Series      | Facebook totals           |
| Describe groups       | `df.groupby('Company').describe()`            | DataFrame   | stats per company         |

---

## 🟢 Section 7: Merge & Join

```python
df1 = pd.DataFrame({'Name':['Alice','Bob','Charlie'],'Age':[25,30,28],'City':['New York','Chicago','Boston']})
df2 = pd.DataFrame({'Name':['Alice','Bob','Eva'],'Salary':[70000,80000,95000]})
```

### Quick Reference — Merge & Join

| Action           | Code Example                                        | Output Type | Example Output          |
| ---------------- | --------------------------------------------------- | ----------- | ----------------------- |
| Concatenate rows | `pd.concat([df1, df2])`                             | DataFrame   | rows stacked            |
| Concatenate cols | `pd.concat([df1, df2], axis=1)`                     | DataFrame   | side-by-side            |
| Merge inner      | `pd.merge(df1, df2, on='Name')`                     | DataFrame   | Alice & Bob with salary |
| Merge outer      | `pd.merge(df1, df2, on='Name', how='outer')`        | DataFrame   | includes Charlie & Eva  |
| Join on index    | `df1.set_index('Name').join(df2.set_index('Name'))` | DataFrame   | joins by Name index     |

---

# ✅ Key Takeaways

* `Series` = one-dimensional labeled array (like a column).
* `DataFrame` = table of rows and columns.
* Indexing with `.loc` (labels) vs `.iloc` (positions).
* Handle missing values with `.dropna()`, `.fillna()`.
* Use `.groupby()` for aggregation.
* Combine datasets with `concat`, `merge`, `join`.
