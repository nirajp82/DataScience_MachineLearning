# 📘 Merging, Joining, and Concatenating DataFrames in Pandas

## 📑 Table of Contents

* [Introduction](#-introduction)
* [Quick Reference Table](#-quick-reference-table)
* [Creating Example DataFrames](#-creating-example-dataframes)
* [Concatenation of DataFrames](#-concatenation-of-dataframes)
* [Merging DataFrames](#-merging-dataframes)
* [Joining DataFrames](#-joining-dataframes)
* [Difference Between Merge and Join](#-difference-between-merge-and-join)
* [Conclusion](#-conclusion)
* [Key Takeaways](#-key-takeaways)

---

## 🔹 Introduction

In real-world projects, employee and company data often live in **separate tables**. Pandas allows you to combine these datasets with:

* **Concatenation (`pd.concat`)** – stack datasets together.
* **Merging (`pd.merge`)** – combine by key columns (like SQL joins).
* **Joining (`.join()`)** – merge by DataFrame indices.

---

## 📊 Quick Reference Table

| Action                   | Code Example                                                | Output Type | Example Output (simplified)                                                            |
| ------------------------ | ----------------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------- |
| Concatenate by rows      | `pd.concat([df1, df2])`                                     | DataFrame   | <pre>Alice 25 New York<br>David 35 San Francisco</pre>                                |
| Concatenate by columns   | `pd.concat([df1, df2], axis=1)`                             | DataFrame   | <pre>Alice 25 New York Bob 30 Chicago</pre>                                           |
| Merge inner join         | `pd.merge(df1, salary_df, on='Name', how='inner')`          | DataFrame   | <pre>Alice 25 New York 70000<br>Bob 30 Chicago 80000</pre>                            |
| Merge left join          | `pd.merge(df1, salary_df, on='Name', how='left')`           | DataFrame   | <pre>Alice 25 New York 70000<br>Charlie 28 Boston NaN</pre>                           |
| Merge right join         | `pd.merge(df1, salary_df, on='Name', how='right')`          | DataFrame   | <pre>Bob 30 Chicago 80000<br>Eva NaN NaN 95000</pre>                                  |
| Merge outer join         | `pd.merge(df1, salary_df, on='Name', how='outer')`          | DataFrame   | <pre>Alice 25 New York 70000<br>Charlie 28 Boston NaN<br>Eva NaN NaN 95000</pre>      |
| Join left (default)      | `df1.set_index('Name').join(dept_df)`                       | DataFrame   | <pre>Alice 25 New York HR<br>Bob 30 Chicago Finance</pre>                             |
| Join right               | `df1.set_index('Name').join(dept_df, how='right')`          | DataFrame   | <pre>Alice 25 New York HR<br>Charlie 28 Boston IT</pre>                               |
| Join outer               | `df1.set_index('Name').join(dept_df, how='outer')`          | DataFrame   | <pre>Alice 25 New York HR<br>Charlie 28 Boston IT<br>David NaN NaN NaN</pre>          |

---

## 🔹 Creating Example DataFrames

```python
import pandas as pd

# Employee basic info
df1 = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 28],
    'City': ['New York', 'Chicago', 'Boston']
})

df2 = pd.DataFrame({
    'Name': ['David', 'Eva'],
    'Age': [35, 40],
    'City': ['San Francisco', 'Seattle']
})

# Salaries
salary_df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'David', 'Eva'],
    'Salary': [70000, 80000, 90000, 95000]
})

# Departments (indexed by employee name)
dept_df = pd.DataFrame({
    'Department': ['HR', 'Finance', 'IT'],
    'Experience': [2, 5, 3]
}, index=['Alice', 'Bob', 'Charlie'])
```

---

## 🔹 Concatenation of DataFrames

```python
pd.concat([df1, df2])
```

**Output:**

```
      Name  Age          City
0    Alice   25      New York
1      Bob   30       Chicago
2  Charlie   28        Boston
0    David   35  San Francisco
1      Eva   40       Seattle
```

---

## 🔹 Merging DataFrames

### Inner Join

```python
pd.merge(df1, salary_df, on='Name', how='inner')
```

**Output:**

```
    Name  Age     City  Salary
0  Alice   25 New York   70000
1    Bob   30  Chicago   80000
```

### Left Join

```python
pd.merge(df1, salary_df, on='Name', how='left')
```

**Output:**

```
      Name  Age     City   Salary
0    Alice   25 New York  70000.0
1      Bob   30  Chicago  80000.0
2  Charlie   28   Boston      NaN
```

### Right Join

```python
pd.merge(df1, salary_df, on='Name', how='right')
```

**Output:**

```
    Name   Age     City  Salary
0  Alice  25.0 New York   70000
1    Bob  30.0  Chicago   80000
2   David   NaN     NaN   90000
3     Eva   NaN     NaN   95000
```

### Outer Join

```python
pd.merge(df1, salary_df, on='Name', how='outer')
```

**Output:**

```
      Name   Age     City   Salary
0    Alice  25.0 New York  70000.0
1      Bob  30.0  Chicago  80000.0
2  Charlie  28.0   Boston      NaN
3    David   NaN     NaN  90000.0
4      Eva   NaN     NaN  95000.0
```

---

## 🔹 Joining DataFrames

### Left Join (default)

```python
df1.set_index('Name').join(dept_df)
```

**Output:**

```
         Age     City Department  Experience
Name                                       
Alice     25 New York        HR           2
Bob       30  Chicago   Finance           5
Charlie   28   Boston        IT           3
```

### Right Join

```python
df1.set_index('Name').join(dept_df, how='right')
```

**Output:**

```
         Age     City Department  Experience
Name                                       
Alice   25.0 New York        HR           2
Bob     30.0  Chicago   Finance           5
Charlie 28.0   Boston        IT           3
```

### Outer Join

```python
df1.set_index('Name').join(dept_df, how='outer')
```

**Output:**

```
          Age          City Department  Experience
Name                                             
Alice    25.0      New York        HR         2.0
Bob      30.0       Chicago   Finance         5.0
Charlie  28.0        Boston        IT         3.0
David     NaN          NaN       NaN         NaN
Eva       NaN          NaN       NaN         NaN
```

---

## 🔹 Difference Between Merge and Join

* **`merge`** → Works on **columns (keys)**, like SQL joins. Example: `pd.merge(df1, df2, on='Name')`
* **`join`** → Works on **index (row labels)**. Example: `df1.set_index('Name').join(df2)`
* **Default behavior**:
  * `merge` → `inner join` (keeps matching rows only)
  * `join` → `left join` (keeps all rows of the left DataFrame)

👉 Think of `merge` = **column-based join**, `join` = **index-based join**.

---

## ✅ Conclusion

* Use **Concatenation** to stack datasets.
* Use **Merge** for column-based joins.
* Use **Join** for index-based joins.
* Always specify `how` (`inner`, `left`, `right`, `outer`) to control the type of join.

---

## 📝 Key Takeaways

* `pd.concat()` → stack rows or columns.
* `pd.merge()` → SQL-style joins on **columns**.
* `.join()` → joins DataFrames on **indices**.
* **Merge = column-based**, **Join = index-based**.
* Always check join type (`inner`, `left`, `right`, `outer`) to avoid data loss.
