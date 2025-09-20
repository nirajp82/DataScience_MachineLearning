## 📑 Table of Contents

* [Part 1 – Introduction to DataFrames](#-pandas-dataframes--part-1)

  * [Introduction & Key Characteristics](#-introduction)
  * [Quick Reference Table (Part 1)](#-part-1-quick-reference)
  * [Quick Reference Table (Part 2)](#-part-2-quick-reference)
  * [Quick Reference Table (Part 3)](#-part-3-quick-reference)
  * [Creating a DataFrame](#-creating-a-dataframe)
  * [Selecting Columns](#-selecting-columns)
  * [Checking Types](#-checking-types)
  * [Creating New Columns](#-creating-new-columns)
  * [Dropping Columns & Rows](#-dropping-columns--rows)
  * [Shape of DataFrame](#-shape-of-dataframe)
  * [Selecting Rows](#-selecting-rows)
  * [Selecting Subsets](#-selecting-subsets)
  * [Key Takeaways](#-key-takeaways)

* [Part 2 – Conditional Selection & Indexing](#-pandas-dataframes--part-2)

  * [Introduction](#-introduction-1)
  * [Quick Reference Table (Part 2)](#-part-2-quick-reference)
  * [Conditional Selection](#-conditional-selection)
  * [Filtering Rows by Column Values](#-filtering-rows-based-on-column-values)
  * [Multiple Conditions](#-multiple-conditions)
  * [Resetting and Setting Index](#-resetting-and-setting-index)
  * [Key Takeaways](#-key-takeaways-1)

* [Part 3 – Multi-Indexed DataFrames](#-pandas-dataframes--part-3)

  * [Introduction](#-introduction-2)
  * [Quick Reference Table (Part 3)](#-part-3-quick-reference)
  * [Creating a MultiIndex](#-creating-a-multiindex)
  * [Accessing Data in MultiIndex](#-accessing-data-in-multiindex)
  * [Naming Index Levels](#-naming-index-levels)
  * [Accessing Specific Values](#-accessing-specific-values)
  * [Cross-Section Method](#-cross-section-method)
  * [Key Takeaways](#-key-takeaways-2)

---

# 📘 Pandas DataFrames – Part 1

## 🔹 Introduction

A **Pandas DataFrame** is a **two-dimensional, size-mutable, and potentially heterogeneous tabular data structure**.
It is the primary data structure in the Pandas library for Python, widely used for data manipulation and analysis.

### **Key Characteristics**

* **Tabular structure** → organizes data into rows & columns (like spreadsheets, SQL tables, or R data.frames).
* **Labeled axes** → rows have **indices**, columns have **names**.
* **Heterogeneous data types** → different columns can store different data types (int, float, string, bool, dates, etc.).
* **Size-mutable** → rows and columns can be added or removed.
* **Built upon Series** → each column is a Pandas **Series**, all sharing the same index.

---
## 📊 Quick Reference Table

#### Part 1 Quick Reference
| Action                        | Code Example                           | Output Type |
| ----------------------------- | -------------------------------------- | ----------- |
| Select single column          | `df['Name']`                           | Series      |
| Select multiple columns       | `df[['Name','Age']]`                   | DataFrame   |
| Check type of selection       | `type(df['Name'])`                     | Series      |
| Add new column                | `df['New'] = df['Age'] + 5`            | DataFrame   |
| Drop column (not inplace)     | `df.drop('New', axis=1)`               | DataFrame   |
| Drop column (permanent)       | `df.drop('New', axis=1, inplace=True)` | None        |
| Drop row                      | `df.drop(1, axis=0)`                   | DataFrame   |
| Shape of DataFrame            | `df.shape`                             | Tuple       |
| Select row by label           | `df.loc[0]`                            | Series      |
| Select row by position        | `df.iloc[2]`                           | Series      |
| Select subset of rows/columns | `df.loc[[0,2], ['Name','City']]`       | DataFrame   |

---

#### Part 2 Quick Reference
| Action                                  | Code Example                           | Output Type |
| --------------------------------------- | -------------------------------------- | ----------- |
| Boolean mask (entire DataFrame)         | `df > 0`                               | DataFrame   |
| Conditional selection (whole DataFrame) | `df[df > 0]`                           | DataFrame   |
| Filter rows (single condition)          | `df[df['W'] > 0]`                      | DataFrame   |
| Filter rows (multiple conditions)       | `df[(df['W'] > 0) & (df['Y'] > 1)]`    | DataFrame   |
| OR condition                            | `df[(df['W'] > 0) | (df['Y'] > 1)]`    | DataFrame   |
| Filter + select column                  | `df[df['W'] > 0]['X']`                 | Series      |
| Filter + select multiple columns        | `df[df['W'] > 0][['Y','X']]`           | DataFrame   |
| Reset index (not inplace)               | `df.reset_index()`                     | DataFrame   |
| Reset index (permanent)                 | `df.reset_index(inplace=True)`         | None        |
| Set column as index                     | `df.set_index('States')`               | DataFrame   |
| Set column as index (permanent)         | `df.set_index('States', inplace=True)` | None        |

---

#### Part 3 Quick Reference
| Action                         | Code Example                                | Output Type |
| ------------------------------ | ------------------------------------------- | ----------- |
| Create multi-index from tuples | `pd.MultiIndex.from_tuples(list_of_tuples)` | MultiIndex  |
| Access outer index             | `df.loc['G1']`                              | DataFrame   |
| Access inner index             | `df.loc['G1'].loc[1]`                       | Series      |
| Check index names              | `df.index.names`                            | list        |
| Set index names                | `df.index.names = ['groups','numb']`        | None        |
| Access specific value          | `df.loc['G2'].loc[2]['b']`                  | Scalar      |
| Cross-section outer level      | `df.xs('G1')`                               | DataFrame   |
| Cross-section inner level      | `df.xs(1, level='numb')`                    | DataFrame   |
```

## 🔹 Creating a DataFrame

```python
import pandas as pd

data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}
df = pd.DataFrame(data)
print(df)
```

**Output:**

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

---

## 🔹 Selecting Columns

```python
df['Name']          # Single column → Series
df[['Name','Age']]  # Multiple columns → DataFrame
```

**Output (single column):**

```
0      Alice
1        Bob
2    Charlie
Name: Name, dtype: object
```

**Output (multiple columns):**

```
      Name  Age
0    Alice   25
1      Bob   30
2  Charlie   35
```

---

## 🔹 Checking Types

```python
type(df['Name'])  # pandas.core.series.Series
type(df)          # pandas.core.frame.DataFrame
```

---

## 🔹 Creating New Columns

```python
df['Age in 5 Years'] = df['Age'] + 5
print(df)
```

**Output:**

```
      Name  Age         City  Age in 5 Years
0    Alice   25     New York              30
1      Bob   30  Los Angeles              35
2  Charlie   35      Chicago              40
```

---

## 🔹 Dropping Columns & Rows

```python
df.drop('Age in 5 Years', axis=1)                 # drops column (not inplace)
df.drop('Age in 5 Years', axis=1, inplace=True)   # drops column permanently
df.drop(1, axis=0)                                # drops row with index 1
```

---

## 🔹 Shape of DataFrame

```python
df.shape
```

**Output:** `(3, 3)`

---

## 🔹 Selecting Rows

```python
df.loc[0]    # by label
df.iloc[2]   # by position
```

---

## 🔹 Selecting Subsets

```python
df.loc[[0,2], ['Name','City']]
```

**Output:**

```
      Name     City
0    Alice  New York
2  Charlie  Chicago
```

---

## ✅ Key Takeaways

* A **DataFrame** = table-like structure (rows × columns).
* Columns are **Series**; one column → Series, multiple → DataFrame.
* Create new columns from existing ones.
* Drop rows/columns with `drop()`.
* Axis: `0` = rows, `1` = columns.
* Row selection: `.loc` (label), `.iloc` (position).
* Subsets via `.loc` with lists.

---

# 📘 Pandas DataFrames – Part 2

## 🔹 Introduction

In this section, we explore **conditional selection** and **indexing** in DataFrames:

* Filtering rows/columns with boolean conditions
* Combining multiple conditions with `&` and `|`
* Resetting and setting custom indices

---

## 🔹 Conditional Selection

```python
bool_df = df > 0
df[bool_df]           # keeps values where True, NaN otherwise
df[df > 0]            # shorthand
```

---

## 🔹 Filtering Rows Based on Column Values

```python
df[df['W'] > 0]       # only rows where W > 0
df[df['Z'] < 0]       # only rows where Z < 0
df[df['W'] > 0]['X']  # filter then grab column
df[df['W'] > 0][['Y','X']] # filter then grab multiple columns
```

---

## 🔹 Multiple Conditions

```python
df[(df['W'] > 0) & (df['Y'] > 1)]   # AND
df[(df['W'] > 0) | (df['Y'] > 1)]   # OR
```

⚠️ Use `&` and `|`, **not** `and` / `or`. Always wrap conditions in parentheses.

---

## 🔹 Resetting and Setting Index

```python
df.reset_index()              # reset index (adds old index as a column)
df.reset_index(inplace=True)  # permanent reset

# Setting new index
df['States'] = 'CA NY WY OR CO'.split()
df.set_index('States')                # temporary
df.set_index('States', inplace=True)  # permanent
```

---

## ✅ Key Takeaways

* Conditional selection = boolean masks + bracket notation.
* Filter rows by applying conditions to columns.
* Combine multiple conditions with `&` (AND), `|` (OR).
* `reset_index()` → back to default integer index.
* `set_index(col)` → assign a column as new index.

---

# 📘 Pandas DataFrames – Part 3

## 🔹 Introduction

In this section, we explore **multi-indexed DataFrames (hierarchical indexing)**:

* Creating multi-level indices
* Accessing data from outer/inner levels
* Naming index levels
* Using `.xs()` cross-section method

---

## 🔹 Creating a MultiIndex

```python
import pandas as pd
import numpy as np

outside = ['G1','G1','G1','G2','G2','G2']
inside  = [1,2,3,1,2,3]
hier_index = pd.MultiIndex.from_tuples(list(zip(outside,inside)))

df = pd.DataFrame(np.random.randn(6,2), index=hier_index, columns=['a','b'])
print(df)
```

**Output (example):**

```
        a         b
G1 1  0.123  -0.456
   2  1.234   0.678
   3 -0.987   0.432
G2 1  0.555  -0.111
   2  0.072   0.890
   3 -1.222   0.333
```

---

## 🔹 Accessing Data in MultiIndex

```python
df.loc['G1']         # all rows under G1
df.loc['G1'].loc[1]  # row 1 under G1
```

---

## 🔹 Naming Index Levels

```python
df.index.names       # [None, None]
df.index.names = ['groups','numb']
print(df)
```

**Output:**

```
groups numb     a     b
G1     1     0.123 -0.456
       2     1.234  0.678
...
```

---

## 🔹 Accessing Specific Values

```python
df.loc['G2'].loc[2]['b']   # example: 0.072
```

---

## 🔹 Cross-Section Method

```python
df.xs('G1')                  # same as df.loc['G1']
df.xs(1, level='numb')       # all rows where numb == 1 across groups
```

---

## ✅ Key Takeaways

* MultiIndex = hierarchical row labels.
* Build with `pd.MultiIndex.from_tuples`.
* Access from **outer → inner** using `.loc`.
* Index levels can be **named**.
* `.xs()` allows cross-section queries at any index level.
