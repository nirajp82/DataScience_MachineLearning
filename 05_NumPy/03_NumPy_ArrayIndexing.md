
# **NumPy Array Selection & Slicing – README**

## Table of Contents

1. [Introduction](#1-introduction)
2. [Creating Arrays](#2-creating-arrays)
3. [Basic Selection (1D Arrays)](#3-basic-selection-1d-arrays)
4. [Broadcasting Values](#4-broadcasting-values)
5. [Indexing 2D Arrays (Matrices)](#5-indexing-2d-arrays-matrices)
6. [Slicing 2D Arrays](#6-slicing-2d-arrays)
7. [Conditional Selection](#7-conditional-selection)
8. [Advanced Slicing Techniques](#8-advanced-slicing-techniques)
9. [Advanced Operations & Best Practices](#9-advanced-operations--best-practices)
10. [Tips & Tricks](#10-tips--tricks)

---

### **1. Introduction**

---

### **2. Creating Arrays**

```python
import numpy as np

# 1D array using arange
arr = np.arange(11)
print(arr)
```

**Output:**

```
[ 0  1  2  3  4  5  6  7  8  9 10 ]
```

---

### **3. Basic Selection (1D Arrays)**

**Selecting a single element**

```python
print(arr[8])
```

**Output:**

```
8
```

**Selecting a range of elements (slice)**

```python
print(arr[1:5])  # index 1 to 4
```

**Output:**

```
[1 2 3 4]
```

**Omitting start or stop**

```python
print(arr[:6])   # 0 to 5
print(arr[5:])   # 5 to end
```

**Output:**

```
[0 1 2 3 4 5]
[5 6 7 8 9 10]
```

---

### **4. Broadcasting Values**

```python
arr[:5] = 100
print(arr)
```

**Output:**

```
[100 100 100 100 100   5   6   7   8   9  10]
```

**Note:** Slices are **views**, not copies. Changes made to a slice directly affect the original array.

**Creating a copy**

```python
arr_copy = arr.copy()
arr_copy[:] = 0
print(arr_copy)
print(arr)
```

**Output:**

```
[0 0 0 0 0 0 0 0 0 0 0]
[100 100 100 100 100   5   6   7   8   9  10]
```

---

### **5. Indexing 2D Arrays (Matrices)**

```python
matrix = np.array([
    [5, 10, 15],
    [20, 25, 30],
    [35, 40, 45]
])
```

**Double bracket notation**

```python
print(matrix[0][0])  # 5
print(matrix[1][1])  # 25
```

**Single bracket + comma notation (recommended)**

```python
print(matrix[1,2])   # 30
```

**Note:** The single-bracket notation `matrix[row, col]` is the standard and more efficient method in NumPy.

---

### **6. Slicing 2D Arrays**

**Selecting rows & columns**

```python
print(matrix[:2, 1:3])  # top-right 2x2
```

**Output:**

```
[[10 15]
 [25 30]]
```

---

### **7. Conditional Selection**

```python
arr2 = np.arange(1, 11)
print(arr2 > 5)  # Boolean array
```

**Output:**

```
[False False False False False  True  True  True  True  True]
```

**Using condition to select**

```python
print(arr2[arr2 > 5])
```

**Output:**

```
[6 7 8 9 10]
```

```python
print(arr2[arr2 < 3])
```

**Output:**

```
[1 2]
```

---

### **8. Advanced Slicing Techniques**

**1. Step size in 2D arrays**

```python
matrix = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9,10,11,12],
    [13,14,15,16]
])

result = matrix[::2, ::2]
print(result)
```

**Output:**

```
[[ 1  3]
 [ 9 11]]
```
•	Syntax: [start:stop:step] → here step (also called stride) controls how many elements to skip.

matrix[::2, ::2]
* Rows: take every 2nd row → 0, 2
* Cols: take every 2nd col → 0, 2
* Result:
* [[ 1  3]
* [ 9 11]]

**2. Negative slicing (reverse order)**

```python
print(matrix[::-1, :])  # reverse rows
print(matrix[:, ::-1])  # reverse columns
```

**Output:**

```
[[13 14 15 16]
 [ 9 10 11 12]
 [ 5  6  7  8]
 [ 1  2  3  4]]

[[ 4  3  2  1]
 [ 8  7  6  5]
 [12 11 10  9]
 [16 15 14 13]]
```

**3. Selecting submatrices**

```python
sub_matrix = matrix[1:3, 1:3]
print(sub_matrix)
```

**Output:**

```
[[ 6  7]
 [10 11]]
```

**4. Skipping rows/columns**

```python
sub_matrix2 = matrix[::2, -2:]
print(sub_matrix2)
```

**Output:**

```
[[ 3  4]
 [11 12]]
```

**5. Combining negative slicing + step**

```python
sub_matrix3 = matrix[::-2, ::2]
print(sub_matrix3)
```

**Output:**

```
[[13 15]
 [ 5  7]]
```

---

### **9. Advanced Operations & Best Practices**

#### **9.1. Element-wise vs. Matrix Multiplication**

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Element-wise multiplication
C = A * B
print("Element-wise multiplication (A * B):\n", C)

# Matrix multiplication
D = A @ B
print("\nMatrix multiplication (A @ B):\n", D)
```

**Output:**

```
Element-wise multiplication (A * B):
[[ 5 12]
 [21 32]]

Matrix multiplication (A @ B):
[[19 22]
 [43 50]]
```

#### **9.2. `np.where()` for Conditional Assignment**

```python
arr_values = np.arange(10)
new_arr = np.where(arr_values < 5, arr_values, 99)
print(new_arr)
```

**Output:**

```
[ 0  1  2  3  4 99 99 99 99 99]
```

#### **9.3. Function vs. Method Syntax**

```python
my_arr = np.array([1, 2, 3])
my_list = [1, 2, 3]

print("Method sum:", my_arr.sum())
print("Function sum:", np.sum(my_arr))
print("Sum of Python list:", np.sum(my_list))
```

**Output:**

```
Method sum: 6
Function sum: 6
Sum of Python list: 6
```

#### **9.4. Data Types (`dtype`)**

```python
float_arr = np.array([1.1, 2.2, 3.3])
int_arr = float_arr.astype(int)
print(int_arr, int_arr.dtype)
```

**Output:**

```
[1 2 3] int64
```

---

### **10. Tips & Tricks**

* Slices are views, not copies. Use `.copy()` for an independent array.
* Use single bracket + comma notation: `matrix[row, col]`.
* Step sizes (`::`) are powerful for skipping elements or reversing arrays.
* Conditional selection is your go-to for filtering data.
* Combine techniques like slicing and boolean indexing for advanced selections.
