# 📘 GroupBy in Pandas: Grouping Data and Aggregation

## 📑 Table of Contents

* [Introduction](#-introduction)
* [Quick Reference Table](#-quick-reference-table)
* [Creating Example Data](#-creating-example-data)
* [Using GroupBy Method](#-using-groupby-method)
* [Aggregate Functions](#-aggregate-functions)
* [Indexing GroupBy Results](#-indexing-groupby-results)
* [Chaining Methods](#-chaining-methods)
* [Describe with GroupBy](#-describe-with-groupby)
* [Conclusion](#-conclusion)
* [Key Takeaways](#-key-takeaways)

---

## 🔹 Introduction

A **GroupBy** operation in Pandas allows you to **split data into groups** based on one or more keys (columns) and then apply **aggregate functions** (like sum, mean, count, etc.) to combine them into summary statistics.

It is one of the most powerful features of Pandas for **data aggregation and analysis**.

---

## 📊 Quick Reference Table

| Action                        | Code Example                                   | Output Type | Example Output (simplified) |
| ----------------------------- | ---------------------------------------------- | ----------- | --------------------------- |
| Create GroupBy object         | `df.groupby('Company')`                        | GroupBy     | GroupBy object              |
| Mean of groups                | `df.groupby('Company').mean()`                 | DataFrame   | Avg sales per company       |
| Sum of groups                 | `df.groupby('Company').sum()`                  | DataFrame   | Total sales per company     |
| Standard deviation            | `df.groupby('Company').std()`                  | DataFrame   | Sales spread per company    |
| Count values                  | `df.groupby('Company').count()`                | DataFrame   | Counts per company          |
| Min / Max values              | `df.groupby('Company').min()` / `.max()`       | DataFrame   | Min/max per column          |
| Access single group aggregate | `df.groupby('Company').sum().loc['Facebook']`  | Series      | Row for Facebook totals     |
| Describe groups               | `df.groupby('Company').describe()`             | DataFrame   | Stats summary per company   |
| Transposed describe           | `df.groupby('Company').describe().transpose()` | DataFrame   | Companies as columns        |

---

## 🔹 Creating Example Data

```python
import pandas as pd

data = {
    'Company': ['Google', 'Google', 'Microsoft', 'Microsoft', 'Facebook', 'Facebook'],
    'Person': ['Sam', 'Charlie', 'Amy', 'Vanessa', 'Carl', 'Sarah'],
    'Sales': [200, 120, 340, 124, 243, 350]
}
df = pd.DataFrame(data)
print(df)
```

**Output:**

```
     Company   Person  Sales
0     Google      Sam    200
1     Google  Charlie    120
2  Microsoft      Amy    340
3  Microsoft   Vanessa    124
4   Facebook     Carl    243
5   Facebook    Sarah    350
```

---

## 🔹 Using GroupBy Method

```python
by_company = df.groupby('Company')
print(by_company)
```

**Output:**

```
<pandas.core.groupby.generic.DataFrameGroupBy object at 0x...>
```

👉 This creates a **GroupBy object**. It doesn’t show results until you apply an **aggregate function**.

---

## 🔹 Aggregate Functions

### Mean

```python
df.groupby('Company').mean()
```

**Output:**

```
             Sales
Company           
Facebook      296.5
Google        160.0
Microsoft     232.0
```

### Sum

```python
df.groupby('Company').sum()
```

**Output:**

```
             Sales
Company           
Facebook        593
Google          320
Microsoft       464
```

### Standard Deviation

```python
df.groupby('Company').std()
```

**Output:**

```
             Sales
Company           
Facebook   75.660426
Google     56.568542
Microsoft 152.735065
```

### Count / Max / Min

```python
df.groupby('Company').count()
df.groupby('Company').max()
df.groupby('Company').min()
```

**Count Output:**

```
           Person  Sales
Company                  
Facebook        2      2
Google          2      2
Microsoft       2      2
```

---

## 🔹 Indexing GroupBy Results

```python
df.groupby('Company').sum().loc['Facebook']
```

**Output:**

```
Sales    593
Name: Facebook, dtype: int64
```

---

## 🔹 Chaining Methods

Instead of saving a GroupBy object first, chain directly:

```python
df.groupby('Company').sum().loc['Facebook']
```

---

## 🔹 Describe with GroupBy

```python
df.groupby('Company').describe()
```

**Output:**

```
           Sales                                            
           count   mean        std    min     25%    50%     75%    max
Company                                                               
Facebook     2.0  296.5  75.660426  243.0  269.75  296.5  323.25  350.0
Google       2.0  160.0  56.568542  120.0  140.00  160.0  180.00  200.0
Microsoft    2.0  232.0 152.735065  124.0  178.00  232.0  286.00  340.0
```

👉 You can **transpose** for readability:

```python
df.groupby('Company').describe().transpose()
```

---

## ✅ Conclusion

The **GroupBy** method in Pandas is used to group rows based on one or more keys and apply aggregate functions. It’s a powerful tool for **data summarization and analysis**.

---

## 📝 Key Takeaways

* `groupby()` splits data into groups and allows applying aggregate functions.
* Common aggregate functions: **sum, mean, count, min, max, std**.
* You can **index results** with `.loc[]`.
* `.describe()` gives detailed stats, `.transpose()` improves readability.
* Best suited for **numeric data**, though works with non-numeric for min/max.

