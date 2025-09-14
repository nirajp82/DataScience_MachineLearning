## **Table of Contents**

1. [Getting Started](#getting-started)
2. [Introduction](#introduction)
3. [Creating Arrays](#creating-arrays)
4. [Array with Array Operations](#array-with-array-operations)
5. [Array with Scalar Operations](#array-with-scalar-operations)
6. [Element-wise vs. Matrix Multiplication](#element-wise-vs-matrix-multiplication)
7. [Logical and Comparison Operations](#logical-and-comparison-operations)
8. [Array Aggregation & The `axis` Parameter](#array-aggregation--the-axis-parameter)
9. [Universal Array Functions (ufuncs)](#universal-array-functions-ufuncs)
10. [Broadcasting Explained](#broadcasting-explained)
11. [Reshaping & Flattening Arrays](#reshaping--flattening-arrays)
12. [Handling `nan` and `inf`](#handling-nan-and-inf)
13. [Common Errors & Warnings](#common-errors--warnings)
14. [Tips & Tricks](#tips--tricks)

---

## **1. Getting Started**

Before using NumPy, ensure it is installed:

```bash
pip install numpy
```

Import NumPy in Python:

```python
import numpy as np
```

---

## **2. Introduction**

This page covers **basic and advanced operations on NumPy arrays**, which are essential for mathematical computations, data analysis, and machine learning workflows.

* Array arithmetic
* Universal functions (ufuncs)
* Broadcasting
* Aggregation
* Reshaping
* Handling `nan` and `inf`
* Tips for efficient coding

---

## **3. Creating Arrays**

```python
# 1D array: 0 to 10
arr = np.arange(11)
print(arr)
```

**Output:**

```
[ 0  1  2  3  4  5  6  7  8  9 10]
```

Other array creation methods:

```python
np.zeros((3,3))       # 3x3 zero matrix
np.ones((2,4))        # 2x4 matrix of ones
np.full((2,3), 7)     # 2x3 matrix filled with 7
np.eye(3)             # 3x3 identity matrix
np.linspace(0,10,5)   # 5 evenly spaced numbers from 0 to 10
```

---

## **4. Array with Array Operations**

NumPy supports **element-wise arithmetic** between arrays of the same shape:

```python
arr1 = np.arange(11)
arr2 = np.arange(11)

print("Addition:", arr1 + arr2)
print("Subtraction:", arr1 - arr2)
print("Multiplication:", arr1 * arr2)
```

**Output:**

```
Addition:       [ 0  2  4  6  8 10 12 14 16 18 20]
Subtraction:    [0 0 0 0 0 0 0 0 0 0 0]
Multiplication: [ 0  1  4  9 16 25 36 49 64 81 100]
```

**Notes:**

* Arrays must have the same shape for element-wise operations.
* Operations are vectorized — faster than Python loops.

---

## **5. Array with Scalar Operations**

A scalar is automatically **broadcast** across the array:

```python
arr = np.arange(11)

print(arr + 100)   # Add 100 to every element
print(arr * 2)     # Multiply every element by 2
print(arr - 50)    # Subtract 50 from every element
```

**Output:**

```
[100 101 102 103 104 105 106 107 108 109 110]
[ 0  2  4  6  8 10 12 14 16 18 20]
[-50 -49 -48 -47 -46 -45 -44 -43 -42 -41 -40]
```

---

## **6. Element-wise vs. Matrix Multiplication**

* `*` → element-wise multiplication
* `@` or `np.dot()` → matrix multiplication (linear algebra)

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print("Element-wise multiplication:\n", A * B)
print("\nMatrix multiplication:\n", A @ B)
```

**Output:**

```
Element-wise multiplication:
 [[ 5 12]
 [21 32]]

Matrix multiplication:
 [[19 22]
 [43 50]]
```

---

## **7. Logical and Comparison Operations**

```python
arr = np.arange(10)

print("Greater than 5:", arr > 5)
print("Equal to 7:", arr == 7)
print("Between 3 and 7:", (arr > 3) & (arr < 7))
```

**Output:**

```
Greater than 5: [False False False False False False  True  True  True  True]
Equal to 7: [False False False False False False False  True False False]
Between 3 and 7: [False False False False  True  True  True False False False]
```

---

## **8. Array Aggregation & The `axis` Parameter**

Aggregation functions summarize arrays. `axis` defines **dimension of operation**:

* `axis=0`: vertical (columns)
* `axis=1`: horizontal (rows)

```python
mat = np.array([[1,2,3],[4,5,6],[7,8,9]])

print("Total sum:", mat.sum())
print("Sum of columns (axis=0):", mat.sum(axis=0))
print("Sum of rows (axis=1):", mat.sum(axis=1))
print("Mean:", mat.mean())
print("Standard deviation of rows:", mat.std(axis=1))
```

**Output:**

```
Total sum: 45
Sum of columns (axis=0): [12 15 18]
Sum of rows (axis=1): [ 6 15 24]
Mean: 5.0
Standard deviation of rows: [0.81649658 0.81649658 0.81649658]
```

**Other aggregation functions:** `np.min()`, `np.max()`, `np.prod()`, `np.cumsum()`, `np.cumprod()`

---

## **9. Universal Array Functions (ufuncs)**

NumPy provides vectorized math functions:

```python
arr = np.array([0,1,4,9,16])

print("sqrt:", np.sqrt(arr))
print("exp:", np.exp(arr))
print("log:", np.log(arr))  # Warning for log(0)
```

**Output:**

```
sqrt: [0. 1. 2. 3. 4.]
exp: [1.00000000e+00 2.71828183e+00 5.45981500e+01 8.10308393e+03 8.88611052e+06]
log: [-inf  0.         1.38629436 2.19722458 2.77258872]
```

**Tips:** Check [NumPy ufuncs documentation](https://numpy.org/doc/stable/reference/ufuncs.html) for all available functions.

---

## **10. Broadcasting Explained**

Smaller arrays **stretch** automatically to match larger arrays without extra memory.

```python
A = np.array([[1,2,3],[4,5,6]])
B = np.array([10,20,30])

print("Broadcasting A + B:\n", A + B)
```

**Output:**

```
Broadcasting A + B:
 [[11 22 33]
 [14 25 36]]
```

---

## **11. Reshaping & Flattening Arrays**

```python
arr = np.arange(12)

# Reshape to 3x4
print(arr.reshape(3,4))

# Flatten back to 1D
print(arr.flatten())
```

**Output:**

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
[ 0  1  2  3  4  5  6  7  8  9 10 11]
```

---

## **12. Handling `nan` and `inf`**

```python
arr_with_zeros = np.array([0,1,2])

print("Division by zero:", 1 / arr_with_zeros)
```

**Output:**

```
Division by zero: [inf  1.   0.5]
```

**Check for special values:**

```python
np.isnan(arr_with_zeros)
np.isinf(arr_with_zeros)
```

---

## **13. Common Errors & Warnings**

* **Shape mismatch:** occurs when performing element-wise ops or broadcasting incorrectly.
* **Division by zero:** returns `inf` or `nan`, triggers warnings.
* **Invalid log / sqrt:** log(0) → `-inf`, sqrt(negative) → `nan`.

---

## **14. Tips & Tricks**

1. Prefer **vectorized operations** over Python loops for performance.
2. Master the `axis` parameter for aggregation.
3. Always check for **`nan` and `inf`** in your data.
4. Remember **`*` vs `@`**: element-wise vs matrix multiplication.
5. Explore **ufuncs** before writing custom loops.
6. Use **`.reshape()`**, `.flatten()` and **broadcasting** for flexible array operations.

