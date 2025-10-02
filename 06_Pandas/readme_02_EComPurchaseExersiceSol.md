# 📊 Ecommerce Purchases Data Analysis

This project performs exploratory data analysis on a CSV dataset of ecommerce purchases using **Pandas**.

---

## 📁 Dataset

The dataset file is named: **`Ecommerce Purchases`**
It contains 10,000 rows and 14 columns related to purchases made on an ecommerce platform.

---

## 📦 Installation and Setup

Ensure you have **pandas** installed:

```bash
pip install pandas
```

Import pandas and read the CSV file into a DataFrame:

```python
import pandas as pd

ecom = pd.read_csv('Ecommerce Purchases')
```

---

## 🔍 Data Exploration

### 👀 View the Head of the DataFrame

```python
ecom.head()
```

---

## 📈 General Info

### ✅ How many rows and columns are there?

```python
ecom.info()
```

* **Rows**: 10,000
* **Columns**: 14

---

### 💰 What is the average purchase price?

```python
ecom['Purchase Price'].mean()
```

* **Average Purchase Price**: `50.35`

### 📉 What are the highest and lowest purchase prices?

```python
ecom['Purchase Price'].max()
ecom['Purchase Price'].min()
```

* **Highest**: `99.99`
* **Lowest**: `0.00`

---

## 📚 Language and Job Insights

### 🌐 How many people have English ('en') as their language?

```python
ecom[ecom['Language']=='en'].count()
```

* **1098 people**

### ⚖️ How many people have the job title "Lawyer"?

```python
ecom[ecom['Job'] == 'Lawyer'].info()
```

* **30 people**

---

## 🕓 Purchase Timing

### 🌓 AM vs PM Purchases

```python
ecom['AM or PM'].value_counts()
```

* **PM**: 5,068
* **AM**: 4,932

---

## 🏆 Most Common Job Titles

```python
ecom['Job'].value_counts().head(5)
```

1. Interior and spatial designer – 31
2. Lawyer – 30
3. Social researcher – 28
4. Purchasing manager – 27
5. Designer, jewellery – 27

---

## 🎯 Specific Queries

### 🎟️ What was the Purchase Price for Lot "90 WT"?

```python
ecom[ecom['Lot']=='90 WT']['Purchase Price']
```

* **Purchase Price**: `$75.10`

---

### 📧 What is the email of the person with credit card number 4926535242672853?

```python
ecom[ecom["Credit Card"] == 4926535242672853]['Email']
```

* **Email**: `bondellen@williams-garza.com`

---

### 💳 How many purchases used American Express and were above $95?

```python
ecom[(ecom['CC Provider']=='American Express') & (ecom['Purchase Price']>95)].count()
```

* **Count**: 39

---

## 🧠 Harder Questions

### 📅 How many people have a credit card that expires in 2025?

```python
sum(ecom['CC Exp Date'].apply(lambda x: x[3:]) == '25')
```

* **Count**: 1,033

---

### 📨 Top 5 Most Common Email Providers

```python
ecom['Email'].apply(lambda x: x.split('@')[1]).value_counts().head(5)
```

1. hotmail.com – 1638
2. yahoo.com – 1616
3. gmail.com – 1605
4. smith.com – 42
5. williams.com – 37

---
