# 📘 Pandas Series — Introduction, Fundamentals, Examples & Outputs
---
## 1) What is a Pandas `Series`? 
* A **Series** is a **one-dimensional labeled array** built on top of NumPy arrays.
* It combines features of arrays and dictionaries: **ordered values + an index (labels)**.
* Series are the building block for `DataFrame` (columns of a DataFrame are Series).
* Useful features: fast label-based lookup, vectorized ops, automatic alignment by index.
---
## 2) Creating Series — code + output

```python
import numpy as np
import pandas as pd

labels = ['A', 'B', 'C']
my_data = [10, 20, 30]
arr = np.array(my_data)
d = {'A': 10, 'B': 20, 'C': 30}
```

### From a list

```python
pd.Series(my_data)
```

**Output**

```
0    10
1    20
2    30
dtype: int64
```

### From a list with explicit labels

```python
pd.Series(my_data, index=labels)
```

**Output**

```
A    10
B    20
C    30
dtype: int64
```

### From a NumPy array (same as list)

```python
pd.Series(arr, index=labels)
```

**Output**

```
A    10
B    20
C    30
dtype: int64
```

### From a dictionary

```python
pd.Series(d)
```

**Output**

```
A    10
B    20
C    30
dtype: int64
```

### Series holding strings / objects / functions

```python
pd.Series(labels)
```

**Output**

```
0    A
1    B
2    C
dtype: object
```

```python
pd.Series([sum, print, len])
```

**Output**

```
0      <built-in function sum>
1    <built-in function print>
2      <built-in function len>
dtype: object
```

---

## 3) Series internals / useful attributes

Given `s = pd.Series([10,20,30], index=['A','B','C'])`:

* `s.index` → `Index(['A', 'B', 'C'], dtype='object')`
* `s.values` → `array([10, 20, 30])`
* `s.dtype` → `dtype('int64')`
* `s.shape` → `(3,)`
* `s.size` → `3`

(These allow programmatic inspection of the Series.)

---

## 4) Indexing & selection (labels vs positions)

```python
ser1 = pd.Series([1, 2, 3, 4], index=['USA', 'Germany', 'USSR', 'Japan'])
ser1
```
**Output**
```
USA        1
Germany    2
USSR       3
Japan      4
dtype: int64
```

Label-based:

```python
ser1['USA']
```

**Output**

```
1
```

Position-based:

```python
ser1[0]        # can work but prefer .iloc for clarity
```

**Output**

```
1
```

Preferred explicit forms:

```python
ser1.loc['USA']   # label-based
ser1.iloc[0]      # position-based
```

Slicing:

```python
ser1['USA':'USSR']   # label-inclusive slicing for labels
```

**Output**

```
USA        1
Germany    2
USSR       3
dtype: int64
```

Boolean selection:

```python
ser1[ser1 > 2]
```

**Output**

```
USSR     3
Japan    4
dtype: int64
```

---

## 5) Operations & alignment (very important concept)

When you apply vectorized operations between Series, Pandas **aligns by index labels**. If an index label is missing in one Series, the result for that label is `NaN`.

```python
ser1 = pd.Series([1, 2, 3, 4], index=['USA', 'Germany', 'USSR', 'Japan'])
ser2 = pd.Series([1, 2, 5, 4], index=['USA', 'Germany', 'Italy', 'Japan'])
```
**Output**
```
ser1:
USA        1
Germany    2
USSR       3
Japan      4
dtype: int64

ser2:
USA        1
Germany    2
Italy      5
Japan      4
dtype: int64
```

```python
ser1 + ser2
```

**Output**

```
Germany    4.0
Italy      NaN
Japan      8.0
USA        2.0
USSR       NaN
dtype: float64
```
##### 📌 Pandas Series Arithmetic Rules

* **Labels match → values are combined**
  Example: `"USA"` → `1 + 1 = 2`

* **Labels don’t match → result is `NaN`**
  Example: `"USSR"` only in `ser1`, `"Italy"` only in `ser2` → `NaN`

* **Result index = union of both indices**
  → all labels from both Series show up

* **Dtype promotion**

  * All labels match and all results are integers → dtype stays int64
  * If any label is missing (NaN appears) → dtype becomes float64 (because `NaN` can’t exist in pure `int64`)
  * **Division (`/`) always returns `float64`**, even if no `NaN`

### Example: dtype promotion on division

```python
s = pd.Series([1, 2, 3])
s / 2
```

**Output**

```
0    0.5
1    1.0
2    1.5
dtype: float64
```

---

## 6) Missing values (NaN) and helpers

```python
s1 = pd.Series([1, 2, None, 4], index=['a','b','c','d'])
s1
```

**Output**

```
a    1.0
b    2.0
c    NaN
d    4.0
dtype: float64
```

Common helpers:

* `s.isnull()` / `s.notnull()`
* `s.dropna()` → remove missing values
* `s.fillna(value)` → replace missing values
* `s.interpolate()` → numeric interpolation (if sensible)

Example:

```python
s1.fillna(0)
```

**Output**

```
a    1.0
b    2.0
c    0.0
d    4.0
dtype: float64
```

---

## 7) Reindexing and explicit alignment

```python
s = pd.Series([10, 20], index=['A','B'])
s.reindex(['A','B','C'])
```

**Output**

```
A    10.0
B    20.0
C     NaN
dtype: float64
```

You can set a fill value:

```python
s.reindex(['A','B','C'], fill_value=0)
```

**Output**

```
A    10
B    20
C     0
dtype: int64
```

---

## 8) Useful methods (quick summary)

##### 1️:`head(n)` — first n rows

```python
ser1.head(2)
```

**Output**

```
USA        1
Germany    2
dtype: int64
```

---

##### 2️:`tail(n)` — last n rows

```python
ser1.tail(2)
```

**Output**

```
USSR    3
Japan   4
dtype: int64
```

---

##### 3️:`describe()` — summary stats

```python
ser1.describe()
```

**Output**

```
count    4.000000
mean     2.500000
std      1.290994
min      1.000000
25%      1.750000
50%      2.500000
75%      3.250000
max      4.000000
dtype: float64
```

---

##### 4️:`value_counts()` — counts of each value

```python
ser1.value_counts()
```

**Output**

```
1    1
2    1
3    1
4    1
dtype: int64
```

---

##### 5️:`sort_index()` — sort by index

```python
ser1.sort_index()
```

**Output**

```
Germany    2
Japan      4
USA        1
USSR       3
dtype: int64
```

##### `sort_values()` — sort by values

```python
ser1.sort_values()
```

**Output**

```
USA       1
Germany   2
USSR      3
Japan     4
dtype: int64
```

---

##### 6️:`astype(dtype)` — convert dtype

```python
ser1.astype(float)
```

**Output**

```
USA       1.0
Germany   2.0
USSR      3.0
Japan     4.0
dtype: float64
```

---

##### 7️: Metadata

```python
ser1.index
```

```
Index(['USA', 'Germany', 'USSR', 'Japan'], dtype='object')
```

```python
ser1.values
```

```
array([1, 2, 3, 4])
```

```python
ser1.name
```

```
None
```

---

##### 8️: `to_dict()` — convert to dictionary

```python
ser1.to_dict()
```

```
{'USA': 1, 'Germany': 2, 'USSR': 3, 'Japan': 4}
```

---

##### 9️: `unique()` — unique values

```python
ser1.unique()
```

```
array([1, 2, 3, 4])
```

##### `nunique()` — count of unique values

```python
ser1.nunique() # Output: 4
```
## 9) Quick practical examples (copy/paste + outputs)

### Example A — simple arithmetic & access

```python
s = pd.Series([10, 20, 30], index=['A','B','C'])
s2 = pd.Series({'A': 100, 'B': 200, 'C': 300})

print(s['A'])   # label access
print(s[0])     # position access
print(s + s2)
```

**Output**

```
10
10
A    110
B    220
C    330
dtype: int64
```

### Example B — boolean and loc/iloc

```python
s = pd.Series([5, 10, 15], index=['x','y','z'])
s.loc['y']
s.iloc[1]
s[s > 7]
```
**Outputs**
```
10
10
y    10
z    15
dtype: int64
```
## 10) Final notes (why Series matter)

* Series provide labeled, index-aware 1D data structures — operations are fast and expressive.
* Understanding Series (indexing, alignment, missing values, dtype promotion) is essential because DataFrame columns behave like Series — everything scales up from here.

