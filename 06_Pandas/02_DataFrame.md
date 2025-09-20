# 📘 Pandas DataFrames

## 📑 Table of Contents
* [Introduction & Key Characteristics](#-introduction)
* [Quick Reference Tables](#-quick-reference-tables)

  * [Part 1 – Basic Operations](#part-1-quick-reference)
  * [Part 2 – Conditional Selection & Indexing](#part-2-quick-reference)
  * [Part 3 – MultiIndex DataFrames](#part-3-quick-reference)

* [Part 1 – Introduction to DataFrames](#-pandas-dataframes--part-1)

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
  * [Conditional Selection](#-conditional-selection)
  * [Filtering Rows by Column Values](#-filtering-rows-based-on-column-values)
  * [Multiple Conditions](#-multiple-conditions)
  * [Resetting and Setting Index](#-resetting-and-setting-index)
  * [Key Takeaways](#-key-takeaways-1)

* [Part 3 – Multi-Indexed DataFrames](#-pandas-dataframes--part-3)

  * [Introduction](#-introduction-2)
  * [Creating a MultiIndex](#-creating-a-multiindex)
  * [Accessing Data in MultiIndex](#-accessing-data-in-multiindex)
  * [Naming Index Levels](#-naming-index-levels)
  * [Accessing Specific Values](#-accessing-specific-values)
  * [Cross-Section Method](#-cross-section-method)
  * [Key Takeaways](#-key-takeaways-2)
---

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

## 📊 Quick Reference Tables

### Part 1 Quick Reference

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

**DataFrame (`df`):**

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

---

# 📊 Quick Reference – Part 1

| Action                        | Code Example                           | Output Type | Example Output                                 |
| ----------------------------- | -------------------------------------- | ----------- | ---------------------------------------------- |
| Select single column          | `df['Name']`                           | Series      | `0 Alice; 1 Bob; 2 Charlie`                    |
| Select multiple columns       | `df[['Name','Age']]`                   | DataFrame   | `[['Alice',25],['Bob',30],['Charlie',35]]`     |
| Check type of selection       | `type(df['Name'])`                     | Series      | `<class 'pandas.core.series.Series'>`          |
| Add new column                | `df['New'] = df['Age'] + 5`            | DataFrame   | Adds `"New"` column with values `[30, 35, 40]` |
| Drop column (not inplace)     | `df.drop('New', axis=1)`               | DataFrame   | Returns DataFrame without `"New"`              |
| Drop column (permanent)       | `df.drop('New', axis=1, inplace=True)` | None        | Removes `"New"` permanently                    |
| Drop row                      | `df.drop(1, axis=0)`                   | DataFrame   | Removes Bob’s row                              |
| Shape of DataFrame            | `df.shape`                             | Tuple       | `(3, 3)`                                       |
| Select row by label           | `df.loc[0]`                            | Series      | Alice row as Series                            |
| Select row by position        | `df.iloc[2]`                           | Series      | Charlie row as Series                          |
| Select subset of rows/columns | `df.loc[[0,2], ['Name','City']]`       | DataFrame   | Alice + Charlie, only Name & City              |

---

# 📊 Quick Reference – Part 2

| Action                                  | Code Example                                       | Output Type | Example Output                            |
| --------------------------------------- | -------------------------------------------------- | ----------- | ----------------------------------------- |
| Boolean mask (entire DataFrame)         | `df > 25`                                          | DataFrame   | Shows `True/False` where condition met    |
| Conditional selection (whole DataFrame) | `df[df['Age'] > 25]`                               | DataFrame   | Bob & Charlie rows                        |
| Filter rows (multiple conditions)       | `df[(df['Age'] > 25) & (df['City']=="Chicago")]`   | DataFrame   | Charlie only                              |
| OR condition                            | `df[(df['Age'] > 25) \| (df['City']=="New York")]` | DataFrame   | Alice + Bob + Charlie (since Alice is NY) |
| Filter + select column                  | `df[df['Age'] > 25]['Name']`                       | Series      | `1 Bob; 2 Charlie`                        |
| Filter + select multiple columns        | `df[df['Age'] > 25][['Name','City']]`              | DataFrame   | Bob and Charlie rows with only Name + City columns.            |
| Reset index (not inplace)               | `df.reset_index()`                                 | DataFrame   | Resets to default 0,1,2 index             |
| Reset index (permanent)                 | `df.reset_index(inplace=True)`                     | None        | Modifies DataFrame index                  |
| Set column as index                     | `df.set_index('Name')`                             | DataFrame   | Uses `Name` as index                      |
| Set column as index (permanent)         | `df.set_index('Name', inplace=True)`               | None        | Same but permanent                        |

---

# 📊 Quick Reference – Part 3

(using MultiIndex example)

```python
import numpy as np

outside = ['G1','G1','G1','G2','G2','G2']
inside  = [1,2,3,1,2,3]
hier_index = pd.MultiIndex.from_tuples(list(zip(outside,inside)))

df_multi = pd.DataFrame(np.random.randn(6,2), index=hier_index, columns=['a','b'])
df_multi.index.names = ['groups','numb']
print(df_multi)
```

**DataFrame (`df_multi`):**

```
              a         b
groups numb              
G1     1    0.12     0.34
       2   -0.56    -1.23
       3    1.45     0.67
G2     1   -0.78     0.45
       2    0.23    -0.12
       3    0.89     1.34
```

| Action                         | Code Example                                | Output Type | Example Output                       |
| ------------------------------ | ------------------------------------------- | ----------- | ------------------------------------ |
| Create multi-index from tuples | `pd.MultiIndex.from_tuples(list_of_tuples)` | MultiIndex  | `MultiIndex([('G1',1),('G1',2)...])` |
| Access outer index             | `df_multi.loc['G1']`                        | DataFrame   | Rows under G1 only                   |
| Access inner index             | `df_multi.loc['G1'].loc[1]`                 | Series      | Row for G1,1                         |
| Check index names              | `df_multi.index.names`                      | list        | `['groups','numb']`                  |
| Set index names                | `df_multi.index.names=['groups','numb']`    | None        | Assigns names to levels              |
| Access specific value          | `df_multi.loc['G2'].loc[2]['b']`            | Scalar      | Single float (e.g., `-0.12`)         |
| Cross-section outer level      | `df_multi.xs('G1')`                         | DataFrame   | All rows under G1                    |
| Cross-section inner level      | `df_multi.xs(1, level='numb')`              | DataFrame   | All rows where numb==1               |
----
# 📘 Pandas DataFrames – Part 1

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

**Output:**

```
<class 'pandas.core.series.Series'>
<class 'pandas.core.frame.DataFrame'>
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

**Output (after dropping row index 1):**

```
      Name  Age      City
0    Alice   25  New York
2  Charlie   35   Chicago
```

---

## 🔹 Shape of DataFrame

```python
df.shape
```

**Output:**

```
(3, 3)
```

---

## 🔹 Selecting Rows

```python
df.loc[0]    # by label
df.iloc[2]   # by position
```

**Output (`df.loc[0]`):**

```
Name       Alice
Age           25
City    New York
Name: 0, dtype: object
```

**Output (`df.iloc[2]`):**

```
Name     Charlie
Age           35
City     Chicago
Name: 2, dtype: object
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

🔗 [Back to Quick Reference](#part-1-quick-reference)
---

# 📘 Pandas DataFrames – Part 2

## 🔹 Introduction

In Part 2, we focus on **conditional selection, filtering, and indexing** with a Pandas DataFrame.
This allows us to extract subsets of rows/columns based on logical conditions and also manage indices.

We continue with our same DataFrame:

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

<details>
<summary>Output</summary>

```
      Name  Age         City
0    Alice   25     New York
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

</details>

---

## 🔹 Conditional Selection

```python
# Boolean mask (check condition)
df['Age'] > 28
```

<details>
<summary>Output</summary>

```
0    False
1     True
2     True
Name: Age, dtype: bool
```

</details>

```python
# Filter rows where Age > 28
df[df['Age'] > 28]
```

<details>
<summary>Output</summary>

```
      Name  Age         City
1      Bob   30  Los Angeles
2  Charlie   35      Chicago
```

</details>

---

## 🔹 Multiple Conditions

```python
# AND condition (Age > 28 AND City == 'Chicago')
df[(df['Age'] > 28) & (df['City'] == 'Chicago')]
```

<details>
<summary>Output</summary>

```
      Name  Age     City
2  Charlie   35  Chicago
```

</details>

```python
# OR condition (Age < 30 OR City == 'Chicago')
df[(df['Age'] < 30) | (df['City'] == 'Chicago')]
```

<details>
<summary>Output</summary>

```
      Name  Age     City
0    Alice   25  New York
2  Charlie   35  Chicago
```

</details>

---

## 🔹 Resetting & Setting Index

```python
# Reset index (creates new index, keeps old as column)
df_reset = df.reset_index()
print(df_reset)
```

<details>
<summary>Output</summary>

```
   index     Name  Age         City
0      0    Alice   25     New York
1      1      Bob   30  Los Angeles
2      2  Charlie   35      Chicago
```

</details>

```python
# Set 'Name' as index
df_name_index = df.set_index('Name')
print(df_name_index)
```

<details>
<summary>Output</summary>

```
         Age         City
Name                     
Alice     25     New York
Bob       30  Los Angeles
Charlie   35      Chicago
```

</details>

---

## 🔑 Key Takeaways

* Use **boolean masks** for filtering (`df[df['Age'] > 28]`).
* Combine conditions with `&` (AND) and `|` (OR).
* **Reset index** when needed for clean indexing.
* **Set a column as index** for more meaningful labels.

🔗 [Back to Quick Reference](#-quick-reference-tables)

---

# 📘 Pandas DataFrames – Part 3

## 🔹 Introduction

Part 3 introduces **MultiIndex DataFrames** (hierarchical indexing).
This allows more complex data organization with multiple levels of indices.

We’ll extend our same dataset to create a **MultiIndex**.

---

## 🔹 Creating MultiIndex

```python
# Create a MultiIndex from Name and City
df_multi = df.set_index(['Name', 'City'])
print(df_multi)
```

<details>
<summary>Output</summary>

```
                 Age
Name    City        
Alice   New York   25
Bob     Los Angeles 30
Charlie Chicago    35
```

</details>

---

## 🔹 Accessing Data in MultiIndex

```python
# Access all data for Alice
df_multi.loc['Alice']
```

<details>
<summary>Output</summary>

```
          Age
City         
New York   25
```

</details>

```python
# Access specific value (Charlie's Age in Chicago)
df_multi.loc[('Charlie', 'Chicago'), 'Age']
```

<details>
<summary>Output</summary>

```
35
```

</details>

---

## 🔹 Naming Index Levels

```python
# Check current index names
print(df_multi.index.names)
```

<details>
<summary>Output</summary>

```
['Name', 'City']
```

</details>

```python
# Rename index levels
df_multi.index.names = ['Person', 'Location']
print(df_multi)
```

<details>
<summary>Output</summary>

```
                  Age
Person  Location     
Alice   New York    25
Bob     Los Angeles 30
Charlie Chicago     35
```

</details>

---

## 🔹 Cross-Section with `xs()`

```python
# Cross-section by outer level
df_multi.xs('Alice')
```

<details>
<summary>Output</summary>

```
          Age
Location     
New York   25
```

</details>

```python
# Cross-section by inner level
df_multi.xs('Chicago', level='Location')
```

<details>
<summary>Output</summary>

```
         Age
Person      
Charlie   35
```

</details>

---

## 🔑 Key Takeaways

* MultiIndex allows **hierarchical indexing** with multiple levels.
* Access data with `.loc[()]` using tuples.
* Index levels can be **renamed** for clarity.
* `.xs()` is a powerful method to slice by a specific index level.

🔗 [Back to Quick Reference](#-quick-reference-tables)


