# ⚙️ Pandas Operations

## 📑 Table of Contents

1. [Introduction](#-introduction)
2. [Quick Reference Table](#-quick-reference-table)
3. [Creating Example DataFrame](#-creating-example-dataframe)
4. [Finding Unique Values](#-finding-unique-values)
5. [Conditional Selection](#-conditional-selection)
6. [Apply Method](#-apply-method)
7. [Removing Columns](#-removing-columns)
8. [Retrieving Column & Index Names](#-retrieving-column--index-names)
9. [Sorting and Ordering](#-sorting-and-ordering)
10. [Finding Null Values](#-finding-null-values)
11. [Pivot Tables](#-pivot-tables)
12. [Conclusion](#-conclusion)
13. [Key Takeaways](#-key-takeaways)

---

## 🔹 Introduction

This section reviews essential **operations in Pandas**, including unique values, conditional selection, applying functions, dropping columns, sorting, null checks, and pivot tables. These tools are crucial for everyday data analysis.

---

## 📊 Quick Reference Table

| Action                | Code Example                                                | Output Type | Example Output                                                                                                                       |
| --------------------- | ----------------------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Unique values         | `df['col2'].unique()`                                       | ndarray     | <pre>\[4 5 6]</pre>                                                                                                                  |
| Number of unique vals | `df['col2'].nunique()`                                      | int         | <pre>3</pre>                                                                                                                         |
| Value counts          | `df['col2'].value_counts()`                                 | Series      | <pre>4    2<br>5    1<br>6    1<br>Name: col2, dtype: int64</pre>                                                                    |
| Conditional select    | `df[df['col1'] > 2]`                                        | DataFrame   | <pre>   col1  col2 col3<br>2     3     6    c<br>3     4     4    d</pre>                                                            |
| Combined condition    | `df[(df['col1'] > 2) & (df['col2']==4)]`                    | DataFrame   | <pre>   col1  col2 col3<br>3     4     4    d</pre>                                                                                  |
| Apply custom func     | `df['col1'].apply(lambda x: x*2)`                           | Series      | <pre>0    2<br>1    4<br>2    6<br>3    8<br>Name: col1, dtype: int64</pre>                                                          |
| Drop a column         | `df.drop('col1', axis=1)`                                   | DataFrame   | <pre>   col2 col3<br>0     4    a<br>1     5    b<br>2     6    c<br>3     4    d</pre>                                              |
| Column names          | `df.columns`                                                | Index       | <pre>Index(\['col1', 'col2', 'col3'], dtype='object')</pre>                                                                          |
| Index names           | `df.index`                                                  | RangeIndex  | <pre>RangeIndex(start=0, stop=4, step=1)</pre>                                                                                       |
| Sort values           | `df.sort_values(by='col2')`                                 | DataFrame   | <pre>   col1  col2 col3<br>0     1     4    a<br>3     4     4    d<br>1     2     5    b<br>2     3     6    c</pre>                |
| Null values check     | `df.isnull()`                                               | DataFrame   | <pre>   col1  col2  col3<br>0  False False False<br>1  False False False<br>2  False False False<br>3  False False False</pre>       |
| Pivot table           | `df2.pivot_table(values='D', index=['A','B'], columns='C')` | DataFrame   | <pre>C        X     Y<br>A   B            <br>bar 1  30.0   NaN<br>    2   NaN  40.0<br>foo 1  10.0   NaN<br>    2   NaN  20.0</pre> |

---

## 🔹 Creating Example DataFrame

```python
import pandas as pd

df = pd.DataFrame({
    'col1': [1, 2, 3, 4],
    'col2': [4, 5, 6, 4],
    'col3': ['a', 'b', 'c', 'd']
})
print(df)
```

**Output:**

```
   col1  col2 col3
0     1     4    a
1     2     5    b
2     3     6    c
3     4     4    d
```

---

## 🔹 Finding Unique Values

```python
df['col2'].unique()
df['col2'].nunique()
df['col2'].value_counts()
```

---

## 🔹 Conditional Selection

```python
df[df['col1'] > 2]
df[(df['col1'] > 2) & (df['col2'] == 4)]
```

---

## 🔹 Apply Method

```python
def times2(x):
    return x * 2

df['col1'].apply(times2)
df['col3'].apply(len)
df['col2'].apply(lambda x: x * 2)
```

---

## 🔹 Removing Columns

```python
df.drop('col1', axis=1)
```

---

## 🔹 Retrieving Column & Index Names

```python
df.columns
df.index
```

---

## 🔹 Sorting and Ordering

```python
df.sort_values(by='col2')
```

---

## 🔹 Finding Null Values

```python
df.isnull()
```

---

## 🔹 Pivot Tables

```python
df2 = pd.DataFrame({
    'A': ['foo', 'foo', 'bar', 'bar'],
    'B': [1, 2, 1, 2],
    'C': ['X', 'Y', 'X', 'Y'],
    'D': [10, 20, 30, 40]
})

df2.pivot_table(values='D', index=['A', 'B'], columns=['C'])
```

---

## ✅ Conclusion

Pandas offers a wide range of built-in operations to explore, filter, transform, and summarize data efficiently.

---

## 📝 Key Takeaways

* `.unique()`, `.nunique()`, `.value_counts()` help explore values.
* Boolean conditions allow flexible **row filtering**.
* `.apply()` with custom or lambda functions unlocks advanced transformations.
* `.drop()` removes columns; `.columns` and `.index` inspect structure.
* `.sort_values()` reorders rows.
* `.isnull()` detects missing values.
* `.pivot_table()` enables Excel-like pivoting.

