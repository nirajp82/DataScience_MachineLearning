# 📂 Data Input and Output with Pandas

## 📑 Table of Contents

1. [Introduction](#-introduction)
2. [Quick Reference Table](#-quick-reference-table)
3. [Reading and Writing CSV Files](#-reading-and-writing-csv-files)
4. [Reading and Writing Excel Files](#-reading-and-writing-excel-files)
5. [Reading HTML Tables](#-reading-html-tables)
6. [Working with SQL Databases](#-working-with-sql-databases)
7. [Working with JSON Data](#-working-with-json-data)
8. [Working with Pickle Files](#-working-with-pickle-files)
9. [Conclusion](#-conclusion)
10. [Key Takeaways](#-key-takeaways)

---

## 🔹 Introduction

Pandas provides flexible tools to **read and write data** across multiple formats:

* 📄 **CSV files**
* 📊 **Excel spreadsheets**
* 🌐 **HTML tables from the web**
* 🗄 **SQL databases**
* 🌍 **JSON files**
* 📦 **Pickle files**

These operations are essential for real-world data science workflows.

---

## 📊 Quick Reference Table

| Action        | Code Example                                            | Output Type | Example Output (simplified)                                                                  |
| ------------- | ------------------------------------------------------- | ----------- | -------------------------------------------------------------------------------------------- |
| Read CSV      | `pd.read_csv('employees.csv')`                          | DataFrame   | <pre>   ID   Name Dept  Salary<br>0 101 Alice   HR   50000<br>1 102   Bob   IT   60000</pre> |
| Write CSV     | `df.to_csv('output.csv', index=False)`                  | File        | Writes CSV file without index column                                                         |
| Read Excel    | `pd.read_excel('employees.xlsx', sheet_name='Sheet1')`  | DataFrame   | <pre>   ID   Name Dept  Salary<br>0 101 Alice   HR   50000<br>1 102   Bob   IT   60000</pre> |
| Write Excel   | `df.to_excel('output.xlsx', sheet_name='Summary')`      | File        | Creates Excel file with custom sheet                                                         |
| Read HTML     | `pd.read_html('https://example.com/table')[0]`          | DataFrame   | <pre>   Bank Name   City   State<br>0   ABC Bank   NY   NY</pre>                             |
| Write to SQL  | `df.to_sql('my_table', engine)`                         | SQL Table   | Stores DataFrame in SQL database                                                             |
| Read from SQL | `pd.read_sql('my_table', engine)`                       | DataFrame   | <pre>   ID   Name Dept  Salary<br>0 101 Alice   HR   50000<br>1 102   Bob   IT   60000</pre> |
| Read JSON     | `pd.read_json('data.json')`                             | DataFrame   | <pre>   ID   Name Dept  Salary<br>0 101 Alice   HR   50000</pre>                             |
| Write JSON    | `df.to_json('data.json', orient='records', lines=True)` | File        | Writes JSON file                                                                             |
| Read Pickle   | `pd.read_pickle('data.pkl')`                            | DataFrame   | Restores DataFrame from pickle                                                               |
| Write Pickle  | `df.to_pickle('data.pkl')`                              | File        | Saves DataFrame in binary format                                                             |

---

## 🔹 Reading and Writing CSV Files

```python
import pandas as pd

# Reading CSV
df = pd.read_csv('employees.csv')
print(df.head())

# Writing CSV
df.to_csv('employees_output.csv', index=False)
```

**Example `employees.csv`:**

```
ID,Name,Department,Salary
101,Alice,HR,50000
102,Bob,IT,60000
103,Carol,Finance,70000
104,Dave,IT,90000
```

**Output:**

```
    ID   Name Department  Salary
0  101  Alice        HR   50000
1  102    Bob        IT   60000
2  103  Carol   Finance   70000
3  104   Dave        IT   90000
```

---

## 🔹 Reading and Writing Excel Files

```python
# Reading Excel
df = pd.read_excel('employees.xlsx', sheet_name='Sheet1')

# Writing Excel
df.to_excel('employees_summary.xlsx', sheet_name='Summary', index=False)
```

---

## 🔹 Reading HTML Tables

```python
# Requires: lxml, html5lib, beautifulsoup4
tables = pd.read_html('https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/')
print(tables[0].head())
```

**Output (sample):**

```
     Bank Name         City State  CERT Acquiring Institution Closing Date
0   Allied Bank  Mulberry   AR   91   Today's Bank             Sep 23, 2016
1  The Woodbury Banking Co.  Woodbury   GA  11297  United Bank             Aug 19, 2016
```

---

## 🔹 Working with SQL Databases

```python
from sqlalchemy import create_engine

# Create SQLite engine in memory
engine = create_engine('sqlite:///:memory:')

# Write DataFrame to SQL
df.to_sql('employees', engine, index=False)

# Read back from SQL
sql_df = pd.read_sql('employees', engine)
print(sql_df)
```

**Output:**

```
    ID   Name Department  Salary
0  101  Alice        HR   50000
1  102    Bob        IT   60000
2  103  Carol   Finance   70000
3  104   Dave        IT   90000
```

---

## 🔹 Working with JSON Data

```python
# Writing to JSON
df.to_json('employees.json', orient='records', lines=True)

# Reading from JSON
json_df = pd.read_json('employees.json', lines=True)
print(json_df)
```

**Output:**

```
    ID   Name Department  Salary
0  101  Alice        HR   50000
1  102    Bob        IT   60000
2  103  Carol   Finance   70000
3  104   Dave        IT   90000
```

---

## 🔹 Working with Pickle Files

```python
# Writing DataFrame as Pickle
df.to_pickle('employees.pkl')

# Reading Pickle file
pickle_df = pd.read_pickle('employees.pkl')
print(pickle_df)
```

**Output:**

```
    ID   Name Department  Salary
0  101  Alice        HR   50000
1  102    Bob        IT   60000
2  103  Carol   Finance   70000
3  104   Dave        IT   90000
```

---

## ✅ Conclusion

* **CSV** is the most widely used.
* **Excel** is common in business environments.
* **HTML** helps scrape tabular data from the web.
* **SQL** is crucial for database-driven workflows.
* **JSON** is key for APIs and web data.
* **Pickle** is useful for fast local storage of Pandas objects.

---

## 📝 Key Takeaways

* `read_` methods: `read_csv`, `read_excel`, `read_html`, `read_sql`, `read_json`, `read_pickle`.
* `to_` methods: `to_csv`, `to_excel`, `to_sql`, `to_json`, `to_pickle`.
* Extra libraries required:

  * `sqlalchemy` → SQL
  * `lxml`, `html5lib`, `beautifulsoup4` → HTML
* **Pickle is Python-specific** (not human-readable, not cross-language).
* **JSON is lightweight and web-friendly**, ideal for API data exchange.
