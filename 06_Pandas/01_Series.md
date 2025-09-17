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

Notes:

* Result shows union of indices (values aligned by label).
* Because of arithmetic, `int64` may be promoted to `float64` when `NaN` is present or to retain fractional results.

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

* `s.head(n)`, `s.tail(n)` — peek at data
* `s.describe()` — summary stats for numeric series
* `s.value_counts()` — counts for categorical values
* `s.sort_index()` / `s.sort_values()` — sorting
* `s.astype(dtype)` — convert dtype
* `s.index`, `s.values`, `s.name` — metadata
* `s.to_dict()` — convert to dict
* `s.unique()`, `s.nunique()` — unique values

Example: `describe()`

```python
pd.Series([10,20,30,40]).describe()
```

**Output**

```
count     4.000000
mean     25.000000
std      12.909944
min      10.000000
25%      17.500000
50%      25.000000
75%      32.500000
max      40.000000
dtype: float64
```

---

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

