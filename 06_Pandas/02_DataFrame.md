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
emp_df = pd.DataFrame(data)
print(emp_df)
```

**DataFrame (`emp_df`):**

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
| Select single column          | `emp_df['Name']`                           | Series      | `0 Alice; 1 Bob; 2 Charlie`                    |
| Select multiple columns       | `emp_df[['Name','Age']]`                   | DataFrame   | `[['Alice',25],['Bob',30],['Charlie',35]]`     |
| Check type of selection       | `type(emp_df['Name'])`                     | Series      | `<class 'pandas.core.series.Series'>`          |
| Add new column                | `emp_df['New'] = emp_df['Age'] + 5`            | DataFrame   | Adds `"New"` column with values `[30, 35, 40]` |
| Drop column (not inplace)     | `emp_df.drop('New', axis=1)`               | DataFrame   | Returns DataFrame without `"New"`              |
| Drop column (permanent)       | `emp_df.drop('New', axis=1, inplace=True)` | None        | Removes `"New"` permanently                    |
| Drop row                      | `emp_df.drop(1, axis=0)`                   | DataFrame   | Removes Bob’s row                              |
| Shape of DataFrame            | `emp_df.shape`                             | Tuple       | `(3, 3)`                                       |
| Select row by label           | `emp_df.loc[0]`                            | Series      | Alice row as Series                            |
| Select row by position        | `emp_df.iloc[2]`                           | Series      | Charlie row as Series                          |
| Select subset of rows/columns | `emp_df.loc[[0,2], ['Name','City']]`       | DataFrame   | Alice + Charlie, only Name & City              |

---

# 📊 Quick Reference – Part 2

| Action                                  | Code Example                                       | Output Type | Example Output                            |
| --------------------------------------- | -------------------------------------------------- | ----------- | ----------------------------------------- |
| Boolean mask (entire DataFrame)         | `emp_df > 25`                                          | DataFrame   | Shows `True/False` where condition met    |
| Conditional selection (whole DataFrame) | `emp_df[emp_df['Age'] > 25]`                               | DataFrame   | Bob & Charlie rows                        |
| Filter rows (multiple conditions)       | `emp_df[(emp_df['Age'] > 25) & (emp_df['City']=="Chicago")]`   | DataFrame   | Charlie only                              |
| OR condition                            | `emp_df[(emp_df['Age'] > 25) \| (emp_df['City']=="New York")]` | DataFrame   | Alice + Bob + Charlie (since Alice is NY) |
| Filter + select column                  | `emp_df[emp_df['Age'] > 25]['Name']`                       | Series      | `1 Bob; 2 Charlie`                        |
| Filter + select multiple columns        | `emp_df[emp_df['Age'] > 25][['Name','City']]`              | DataFrame   | Bob and Charlie rows with only Name + City columns.            |
| Reset index (not inplace)               | `emp_df.reset_index()`                                 | DataFrame   | Resets to default 0,1,2 index             |
| Reset index (permanent)                 | `emp_df.reset_index(inplace=True)`                     | None        | Modifies DataFrame index                  |
| Set column as index                     | `emp_df.set_index('Name')`                             | DataFrame   | Uses `Name` as index                      |
| Set column as index (permanent)         | `emp_df.set_index('Name', inplace=True)`               | None        | Same but permanent                        |

---

# 📊 Quick Reference – Part 3
```python
import pandas as pd

# Create hierarchical index from City + Name (with duplicate Bob in New York)
arrays = [
    ['New York','New York','New York','Los Angeles','Los Angeles','Chicago','Chicago'],
    ['Alice','Bob','Bob','Charlie','David','Eva','Frank']
]
index = pd.MultiIndex.from_arrays(arrays, names=('City','Name'))

# Create DataFrame
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

---

| Action                         | Code Example                                               | Output Type | Example Output                                                |
| ------------------------------ | ---------------------------------------------------------- | ----------- | ------------------------------------------------------------- |
| Create multi-index from arrays | `pd.MultiIndex.from_arrays(arrays, names=('City','Name'))` | MultiIndex  | `MultiIndex([('New York','Alice'), ('New York','Bob'), ...])` |
| Access outer index             | `emp_df_multi.loc['New York']`                                 | DataFrame   | Rows under **New York** (Alice & 2×Bob)                       |
| Access inner index             | `emp_df_multi.loc['Chicago'].loc['Eva']`                       | Series      | `Age 40, Score 95`                                            |
| Check index names              | `emp_df_multi.index.names`                                     | list        | `['City','Name']`                                             |
| Set index names                | `emp_df_multi.index.names = ['City','Person']`                 | None        | Renames levels to `['City','Person']`                         |
| Access specific value          | `emp_df_multi.loc['Los Angeles'].loc['David']['Score']`        | Scalar      | `85`                                                          |
| Cross-section outer level      | `emp_df_multi.xs('Chicago')`                                   | DataFrame   | All rows under **Chicago** (Eva & Frank)                      |
| Cross-section inner level      | `emp_df_multi.xs('Bob', level='Name')`                         | DataFrame   | All rows where **Name = Bob** (2 rows, New York)              |

---

### 🔎 Note on Duplicate Indices

* Pandas **allows duplicate indices** (both in normal Index and MultiIndex).
* When you call `.loc` with a duplicate key (like `"Bob"`), Pandas will **return all matching rows** instead of a single row.
* This is different from databases (like SQL) where a primary key must be unique.
* Duplicates are useful when modeling real-world data (e.g., multiple people with the same name, multiple entries in the same city).

---

# 📘 Pandas DataFrames – Part 1

## 🔹 Creating a DataFrame

```python
import pandas as pd

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

---

## 🔹 Selecting Columns

```python
emp_df['Name']          # Single column → Series
emp_df[['Name','Age']]  # Multiple columns → DataFrame
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
type(emp_df['Name'])  # pandas.core.series.Series
type(emp_df)          # pandas.core.frame.DataFrame
```

**Output:**

```
<class 'pandas.core.series.Series'>
<class 'pandas.core.frame.DataFrame'>
```

---

## 🔹 Creating New Columns

```python
emp_df['Age in 5 Years'] = emp_df['Age'] + 5
print(emp_df)
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
emp_df.drop('Age in 5 Years', axis=1)                 # drops column (not inplace)
emp_df.drop('Age in 5 Years', axis=1, inplace=True)   # drops column permanently
emp_df.drop(1, axis=0)                                # drops row with index 1
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
emp_df.shape
```

**Output:**

```
(3, 3)
```

---

## 🔹 Selecting Rows

```python
emp_df.loc[0]    # by label
emp_df.iloc[2]   # by position
```

**Output (`emp_df.loc[0]`):**

```
Name       Alice
Age           25
City    New York
Name: 0, dtype: object
```

**Output (`emp_df.iloc[2]`):**

```
Name     Charlie
Age           35
City     Chicago
Name: 2, dtype: object
```

---

## 🔹 Selecting Subsets

```python
emp_df.loc[[0,2], ['Name','City']]
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
emp_df = pd.DataFrame(data)
print(emp_df)
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
emp_df['Age'] > 28
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
emp_df[emp_df['Age'] > 28]
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
emp_df[(emp_df['Age'] > 28) & (emp_df['City'] == 'Chicago')]
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
emp_df[(emp_df['Age'] < 30) | (emp_df['City'] == 'Chicago')]
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
emp_df_reset = emp_df.reset_index()
print(emp_df_reset)
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
emp_df_name_index = emp_df.set_index('Name')
print(emp_df_name_index)
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

* Use **boolean masks** for filtering (`emp_df[emp_df['Age'] > 28]`).
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
emp_df_multi = emp_df.set_index(['Name', 'City'])
print(emp_df_multi)
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
emp_df_multi.loc['Alice']
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
emp_df_multi.loc[('Charlie', 'Chicago'), 'Age']
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
print(emp_df_multi.index.names)
```

<details>
<summary>Output</summary>

```
['Name', 'City']
```

</details>

```python
# Rename index levels
emp_df_multi.index.names = ['Person', 'Location']
print(emp_df_multi)
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

The `.xs()` method is used to **select data at a particular index level** in a MultiIndex DataFrame.
It is especially useful when you want a **clean, direct way** to access rows or columns without writing verbose `.loc` code.

**Why it's useful:**

* Provides a **shortcut** for slicing along a specific index level.
* Makes code **cleaner and easier to read** compared to `.loc` with `slice`.
* Works well when dealing with **hierarchical indices** (MultiIndex).

**Examples:**

```python
# Get all rows where City = 'Chicago'
emp_df_multi.xs('Chicago')
```

```
         Age  Score
Name                
Eva       40     95
Frank     32     90
```

```python
# Get all rows where Name = 'Bob'
emp_df_multi.xs('Bob', level='Name')
```

```
           Age  Score
City                  
New York    30     92
```

**Comparison with `.loc`:**

* Equivalent `.loc` query for the last example:

  ```python
  emp_df_multi.loc[(slice(None), 'Bob'), :]
  ```
* `.xs()` is **shorter and more readable**.
* `.loc` is more **flexible** (multiple conditions, slices, etc.).

👉 **Rule of thumb**: Use `.xs()` for **quick access by one index level**; use `.loc` for **complex selections**.

```python
# Cross-section by outer level
emp_df_multi.xs('Alice')
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
emp_df_multi.xs('Chicago', level='Location')
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


