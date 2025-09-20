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

## 🔹 Creating a DataFrame

```python
import pandas as pd

# Create a DataFrame from a dictionary
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

⚠️ **Note:** Use **bracket notation** (recommended).
Dot notation (`df.Name`) works but may conflict with method names.

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

**Notes:**

* `axis=0` → rows
* `axis=1` → columns
* `inplace=True` → makes the change permanent

---

## 🔹 Shape of DataFrame

```python
df.shape   # (rows, columns)
```

Example: `(3, 3)`

---

## 🔹 Selecting Rows

```python
df.loc[0]    # by label (index 0)
df.iloc[2]   # by position (row at index 2)
```

**Output (row 0):**

```
Name       Alice
Age           25
City    New York
Name: 0, dtype: object
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

* A **DataFrame** is a **table-like structure** (rows × columns).
* Each **column is a Series**; can select one (`df['col']`) or multiple (`df[['c1','c2']]`).
* **New columns** can be created from existing ones.
* **Drop** rows/columns with `drop()`, using `axis` and `inplace`.
* **Axis meanings**: `0` = rows, `1` = columns.
* **Row selection**:

  * `.loc` → by **label**
  * `.iloc` → by **position**
* **Subsets**: `.loc` with lists of row/column labels.

