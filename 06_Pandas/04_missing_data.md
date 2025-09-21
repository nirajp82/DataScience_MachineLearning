Great 🚀 Let’s build the **final polished README** where the **Quick Reference Table** has **Code + Real Output (mini DataFrame previews)** for every example.

---

# 📘 Handling Missing Data in Pandas

## 📑 Table of Contents

* [Introduction](#-introduction)
* [Quick Reference](#-quick-reference)
* [Creating a DataFrame with Missing Values](#-creating-a-dataframe-with-missing-values)
* [Dropping Missing Values with dropna()](#-dropping-missing-values-with-dropna)

  * [Drop Rows with Missing Values](#drop-rows-with-missing-values)
  * [Drop Columns with Missing Values](#drop-columns-with-missing-values)
  * [Drop Rows with Threshold of Non-Null Values](#drop-rows-with-threshold-of-non-null-values)
* [Filling Missing Values with fillna()](#-filling-missing-values-with-fillna)

  * [Fill with Constant Value](#fill-with-constant-value)
  * [Fill with Column Mean](#fill-with-column-mean)
* [Key Takeaways](#-key-takeaways)

---

## 📊 Quick Reference

**Base DataFrame (`df`)**

```python
import pandas as pd
import numpy as np

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [25, np.nan, 30, np.nan, 40],
    'City': ['New York', 'Los Angeles', np.nan, 'Chicago', 'Chicago']
}
df = pd.DataFrame(data)
print(df)
```

| Name    | Age  | City        |
| ------- | ---- | ----------- |
| Alice   | 25.0 | New York    |
| Bob     | NaN  | Los Angeles |
| Charlie | 30.0 | NaN         |
| David   | NaN  | Chicago     |
| Eva     | 40.0 | Chicago     |

---

| Action                                | Code Example                         | Output Type | Example Output                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------- | ------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Drop rows with missing values**     | `df.dropna()`                        | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>                                                                                                                                                                       |
| **Drop columns with missing values**  | `df.dropna(axis=1)`                  | DataFrame   | <table><tr><th>Name</th></tr><tr><td>Alice</td></tr><tr><td>Bob</td></tr><tr><td>Charlie</td></tr><tr><td>David</td></tr><tr><td>Eva</td></tr></table>                                                                                                                                                                                      |
| **Drop rows with ≥2 non-null values** | `df.dropna(thresh=2)`                | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>NaN</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>NaN</td></tr><tr><td>David</td><td>NaN</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>             |
| **Fill missing with constant**        | `df.fillna('Unknown')`               | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>Unknown</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>Unknown</td></tr><tr><td>David</td><td>Unknown</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table> |
| **Fill missing with column mean**     | `df['Age'].fillna(df['Age'].mean())` | Series      | 0 → 25.00<br>1 → 31.67<br>2 → 30.00<br>3 → 31.67<br>4 → 40.00                                                                                                                                                                                                                                                                               |

---

## 🔹 Introduction

Missing data is a common issue in real-world datasets.
In **Pandas**, missing values appear as **NaN**.

Two essential methods help:

* **`dropna()`** → remove missing values.
* **`fillna()`** → replace missing values with constants/statistics.

---

## 🔹 Creating a DataFrame with Missing Values

```python
import pandas as pd
import numpy as np

data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [25, np.nan, 30, np.nan, 40],
    'City': ['New York', 'Los Angeles', np.nan, 'Chicago', 'Chicago']
}
df = pd.DataFrame(data)
df
```

---

## 🔹 Dropping Missing Values with `dropna()`

### Drop Rows with Missing Values

```python
df.dropna()
```

### Drop Columns with Missing Values

```python
df.dropna(axis=1)
```

### Drop Rows with Threshold of Non-Null Values

```python
df.dropna(thresh=2)
```

---

## 🔹 Filling Missing Values with `fillna()`

### Fill with Constant Value

```python
df.fillna('Unknown')
```

### Fill with Column Mean

```python
df['Age'].fillna(df['Age'].mean())
```

---

## 🔹 Key Takeaways

* **`dropna()`** → deletes missing values (row/column).
* **`fillna()`** → replaces missing values with constants/statistics.
* **`axis`** controls row vs column operations.
* **`thresh`** ensures rows/columns have minimum non-null values.
* Proper handling of NaN is critical for clean analysis.

---

👉 This version is a **one-stop cheat sheet**: explanation + real outputs + quick lookup table.

Do you want me to **expand the Quick Reference with both row-wise & column-wise `fillna()` (e.g., filling by forward/backward fill)** for completeness?
