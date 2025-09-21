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
  * [Forward Fill (propagate last valid value)](#forward-fill-propagate-last-valid-value)
  * [Backward Fill (propagate next valid value)](#backward-fill-propagate-next-valid-value)
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

| Action                                         | Code Example                         | Output Type | Example Output                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------- | ------------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Drop rows with missing values**              | `df.dropna()`                        | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>                                                                                                                                                                       |
| **Drop columns with missing values**           | `df.dropna(axis=1)`                  | DataFrame   | <table><tr><th>Name</th></tr><tr><td>Alice</td></tr><tr><td>Bob</td></tr><tr><td>Charlie</td></tr><tr><td>David</td></tr><tr><td>Eva</td></tr></table>                                                                                                                                                                                      |
| **Drop rows with ≥2 non-null values**          | `df.dropna(thresh=2)`                | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>NaN</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>NaN</td></tr><tr><td>David</td><td>NaN</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>             |
| **Fill missing with constant**                 | `df.fillna('Unknown')`               | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>Unknown</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>Unknown</td></tr><tr><td>David</td><td>Unknown</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table> |
| **Fill missing with column mean**              | `df['Age'].fillna(df['Age'].mean())` | Series      | 0 → 25.00<br>1 → 31.67<br>2 → 30.00<br>3 → 31.67<br>4 → 40.00                                                                                                                                                                                                                                                                               |
| **Forward Fill (propagate last valid value)**  | `df.fillna(method='ffill')`          | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>25.0</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>Los Angeles</td></tr><tr><td>David</td><td>30.0</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>   |
| **Backward Fill (propagate next valid value)** | `df.fillna(method='bfill')`          | DataFrame   | <table><tr><th>Name</th><th>Age</th><th>City</th></tr><tr><td>Alice</td><td>25.0</td><td>New York</td></tr><tr><td>Bob</td><td>30.0</td><td>Los Angeles</td></tr><tr><td>Charlie</td><td>30.0</td><td>Chicago</td></tr><tr><td>David</td><td>40.0</td><td>Chicago</td></tr><tr><td>Eva</td><td>40.0</td><td>Chicago</td></tr></table>       |

---

## 🔹 Introduction

Missing data is common in real-world datasets.
In **Pandas**, missing values are represented as **NaN**.

Two key methods help:

* **`dropna()`** → remove missing values.
* **`fillna()`** → replace missing values with constants/statistics/propagation.

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

### Forward Fill (propagate last valid value)

```python
df.fillna(method='ffill')
```

### Backward Fill (propagate next valid value)

```python
df.fillna(method='bfill')
```

---

## 🔹 Key Takeaways

* **`dropna()`** → removes rows/columns with NaN.
* **`fillna()`** → replaces NaN with constants, mean, or propagated values.
* **Forward fill (`ffill`)** carries the last valid value forward.
* **Backward fill (`bfill`)** fills using the next valid value.
* Proper handling of NaN is essential for clean, reliable datasets.
