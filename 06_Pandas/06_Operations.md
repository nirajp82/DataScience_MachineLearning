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

This guide shows how to perform **Pandas operations** using a simple Employee dataset.
We’ll explore unique values, filtering, applying custom functions, sorting, null checks, and pivot tables — all with real-world employee-related examples.

---
## 🔹 Creating Example DataFrame

```python
import pandas as pd

df = pd.DataFrame({
    'EmployeeID': [101, 102, 103, 104],
    'Name': ['Alice', 'Bob', 'Carol', 'Dave'],
    'Department': ['HR', 'IT', 'Finance', 'IT'],
    'Salary': [50000, 60000, 70000, 90000]
})
print(df)
```

**Output:**

```
   EmployeeID   Name Department  Salary
0         101  Alice        HR   50000
1         102    Bob        IT   60000
2         103  Carol   Finance   70000
3         104   Dave        IT   90000
```
---
## 📊 Quick Reference Table

| Action                | Code Example                                                             | Output Type | Example Output                                                                                                                                                                                                              |
| --------------------- | ------------------------------------------------------------------------ | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unique values         | `df['Department'].unique()`                                              | ndarray     | <pre>\['HR' 'IT' 'Finance']</pre>                                                                                                                                                                                           |
| Number of unique vals | `df['Department'].nunique()`                                             | int         | <pre>3</pre>                                                                                                                                                                                                                |
| Value counts          | `df['Department'].value_counts()`                                        | Series      | <pre>IT         2<br>HR         1<br>Finance    1<br>Name: Department, dtype: int64</pre>                                                                                                                                   |
| Conditional select    | `df[df['Salary'] > 60000]`                                               | DataFrame   | <pre>   EmployeeID   Name Department  Salary<br>2           103  Carol    Finance   70000<br>3           104   Dave        IT   90000</pre>                                                                                 |
| Combined condition    | `df[(df['Salary'] > 60000) & (df['Department']=="IT")]`                  | DataFrame   | <pre>   EmployeeID  Name Department  Salary<br>3          104  Dave        IT   90000</pre>                                                                                                                                 |
| Apply custom func     | `df['Salary'].apply(lambda x: x*1.1)`                                    | Series      | <pre>0    55000.0<br>1    66000.0<br>2    77000.0<br>3    99000.0<br>Name: Salary, dtype: float64</pre>                                                                                                                     |
| Drop a column         | `df.drop('Department', axis=1)`                                          | DataFrame   | <pre>   EmployeeID   Name  Salary<br>0         101   Alice   50000<br>1         102     Bob   60000<br>2         103   Carol   70000<br>3         104    Dave   90000</pre>                                                 |
| Column names          | `df.columns`                                                             | Index       | <pre>Index(\['EmployeeID', 'Name', 'Department', 'Salary'], dtype='object')</pre>                                                                                                                                           |
| Index names           | `df.index`                                                               | RangeIndex  | <pre>RangeIndex(start=0, stop=4, step=1)</pre>                                                                                                                                                                              |
| Sort values           | `df.sort_values(by='Salary')`                                            | DataFrame   | <pre>   EmployeeID   Name Department  Salary<br>0         101  Alice        HR   50000<br>1         102    Bob        IT   60000<br>2         103  Carol   Finance   70000<br>3         104   Dave        IT   90000</pre>  |
| Null values check     | `df.isnull()`                                                            | DataFrame   | <pre>   EmployeeID   Name  Department  Salary<br>0      False  False      False   False<br>1      False  False      False   False<br>2      False  False      False   False<br>3      False  False      False   False</pre> |
| Pivot table           | `df2.pivot_table(values='Salary', index='Department', columns='Gender')` | DataFrame   | <pre>Gender       F      M<br>Department             <br>Finance   70000.0    NaN<br>HR        50000.0    NaN<br>IT           NaN  75000.0</pre>                                                                            |

---

## 🔹 Finding Unique Values

```python
df['Department'].unique()
df['Department'].nunique()
df['Department'].value_counts()
```

---

## 🔹 Conditional Selection

```python
# Employees earning more than 60k
df[df['Salary'] > 60000]

# IT employees earning above 60k
df[(df['Salary'] > 60000) & (df['Department'] == 'IT')]
```

---

## 🔹 Apply Method

```python
# Increase salary by 10%
df['Salary'].apply(lambda x: x * 1.1)

# Custom function to add bonus
def add_bonus(salary):
    return salary + 5000

df['Salary'].apply(add_bonus)
```

---

## 🔹 Removing Columns

```python
df.drop('Department', axis=1)
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
df.sort_values(by='Salary')
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
    'Name': ['Alice', 'Bob', 'Carol', 'Dave'],
    'Department': ['HR', 'IT', 'Finance', 'IT'],
    'Gender': ['F', 'M', 'F', 'M'],
    'Salary': [50000, 60000, 70000, 90000]
})

df2.pivot_table(values='Salary', index='Department', columns='Gender')
```

---

## ✅ Conclusion

Using an employee dataset, we saw how Pandas operations help explore, filter, transform, and summarize business data. These techniques are widely applicable in HR analytics, payroll systems, and workforce reporting.

---

## 📝 Key Takeaways

* `.unique()`, `.nunique()`, `.value_counts()` → explore categorical fields like Departments.
* Boolean conditions → filter employees based on Salary or Department.
* `.apply()` → apply salary adjustments or bonuses.
* `.drop()` → remove unnecessary columns.
* `.columns` / `.index` → check dataset structure.
* `.sort_values()` → rank employees by salary.
* `.isnull()` → find missing employee records.
* `.pivot_table()` → summarize salary distributions by Department & Gender.
