# **NumPy Arrays: Examples Explained for Beginners**

---
## Table of Contents

1. [Creating Arrays from Python Lists](#1-creating-arrays-from-python-lists)  
2. [Using `np.arange(start, stop, step)`](#2-using-nparangestart-stop-step)  
3. [Using `np.zeros(shape)`](#3-using-npzerosshape)  
4. [Using `np.ones(shape)`](#4-using-nponesshape)  
5. [`np.linspace(start, stop, num_points)` – Linear Space (evenly spaced numbers)](#5-nplinspacestart-stop-numpoints--linear-space-evenly-spaced-numbers)  
6. [Using `np.eye(n)` – Identity Matrix](#6-using-npeyn--identity-matrix)  
7. [Random Arrays](#7-random-arrays)  
8. [Array Attributes](#8-array-attributes)  
9. [Array Methods](#9-array-methods)  
10. [Vectorized Operations](#10-vectorized-operations)
---

### **1. Creating Arrays from Python Lists**

```python
import numpy as np

arr = np.array([1, 2, 3])           # 1D array (vector)
my_mat = [[1,2,3],[4,5,6],[7,8,9]]
np.array(my_mat) # This converts a nested Python list (list of lists) into a 2D NumPy array (matrix):

Output my_mat: array([[1, 2, 3],
       [4, 5, 6],
       [7, 8, 9]])
```

**Explanation:**

* `np.array([1,2,3])` → creates a **1D array**, similar to a Python list `[1,2,3]`, but faster and supports mathematical operations directly.
* `np.array([[1,2,3],[4,5,6]])` → creates a **2D array (matrix)** with 2 rows and 3 columns. Think of it as a mini spreadsheet.

The reason we **convert a Python list to a NumPy array** is because **NumPy arrays are much more powerful and efficient than Python lists**, especially for AI/ML or numerical computations. Let me explain step by step using your example:

```python
import numpy as np

my_list = [1, 2, 3]   # a regular Python list
numpy_arr = np.array(my_list)  # convert to NumPy array
numpy_arr
```

---

#### **Why convert to NumPy array?**

1.1. **Vectorized Operations**

* With NumPy arrays, arithmetic is element-wise.

```python
# Python list
my_list * 2        # [1, 2, 3, 1, 2, 3] → just repeats list
# NumPy array
numpy_arr * 2           # [2, 4, 6] → multiplies each element

my_list + my_list   # Output: [1, 2, 3, 1, 2, 3] → concatenates lists
numpy_arr + numpy_arr         # Output: [2, 4, 6]         → adds element-wise
```

✅ This is critical in AI/ML where you apply operations to **entire feature vectors or matrices** at once.

1.2. **Better Performance & Memory Efficiency**

* NumPy arrays are stored in **contiguous memory**, unlike Python lists.
* This makes **large numerical computations faster**.

1.3. **Access to Powerful NumPy Functions**

* You can use `.reshape()`, `.sum()`, `.mean()`, `.max()`, `.min()`, etc.

```python
numpy_arr.sum()     # 6
numpy_arr.mean()    # 2.0
numpy_arr.reshape((3,1))  # [[1],[2],[3]]
```

1.4. **Multi-Dimensional Arrays**

* Lists are limited and nested lists become messy for 2D/3D data.
* NumPy handles **matrices and tensors** easily, which is essential in AI/ML.

```python
mat_list = [[1,2],[3,4]]
np_mat = np.array(mat_list)  # 2x2 matrix
```

##### ✅ **Summary**

* **Python list:** simple, flexible, but slow for math on large datasets.
* **NumPy array:** fast, memory-efficient, supports **vectorized math**, and is essential for AI/ML.
* So converting `[1,2,3]` to a NumPy array gives you the **power to do math operations efficiently** on the array.

---

### **2. Using `np.arange(start, stop, step)`**

* The most common way to create a sequence of numbers in NumPy is using `np.arange()`, which works very similarly to Python’s built-in `range()` function.
* The name **`arange`** comes from **“array + range”**.

  * `range()` in Python creates a sequence of numbers.
  * `np.arange()` does the same thing but returns a **NumPy array** instead of a list.

```python
np.arange(0, 10, 2)  # Output: [0, 2, 4, 6, 8]
```

**Explanation:**

* Works **like Python’s `range()` function**, but returns a NumPy array instead of a list.
* `0` → starting number, `10` → stop (does not include 10), `2` → step/increment.
* So it starts at 0, adds 2 each time → `[0, 2, 4, 6, 8]`.

---

### **3. Using `np.zeros(shape)`**

```python
np.zeros(3)       # Output: array([0., 0., 0.])
np.zeros((2,3))   # Output: array([[0., 0., 0.],
                   #               [0., 0., 0.]])
```

**Explanation:**

* Creates arrays **filled with zeros**.
* `3` → 1D array of 3 zeros.
* `(2,3)` → 2 rows and 3 columns of zeros → useful for initializing weights or placeholders in ML.

---

### **4. Using `np.ones(shape)`**

```python
np.ones(4)        # Output: array([1., 1., 1., 1.])
np.ones((3,2))    # Output: array([[1., 1.],
                   #               [1., 1.],
                   #               [1., 1.]])
```

**Explanation:**

* Similar to `zeros`, but fills the array with **ones**.
* `4` → 1D array of 4 ones.
* `(3,2)` → 3 rows and 2 columns of ones.

---

### **5. `np.linspace(start, stop, num_points)` – Linear Space (evenly spaced numbers)**

* The `numpy.linspace()` function generates an array of **evenly spaced numbers** over a specified interval.
* **Syntax:**

```python
numpy.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None, axis=0)
```

**Parameters:**

* `start` → starting value of the sequence
* `stop` → end value of the sequence
* `num` → number of samples to generate (default 50)
* `endpoint` → include `stop` in the array? (default True)
* `retstep` → return step size along with array? (default False)
* `dtype` → data type of the output array
* `axis` → axis to store values if `start` or `stop` are array-like

```python
import numpy as np

# 5 evenly spaced numbers between 0 and 10 (inclusive)
arr1 = np.linspace(0, 10, num=5)
print("Array 1:", arr1)
# Output: array([ 0. ,  2.5,  5. ,  7.5, 10. ])

# 5 evenly spaced numbers between 0 and 10 (excluding 10)
arr2 = np.linspace(0, 10, num=5, endpoint=False)
print("Array 2:", arr2)
# Output: [0. 2. 4. 6. 8.]

# Get step size along with array
arr3, step = np.linspace(0, 10, num=5, retstep=True)
print("Array 3:", arr3)
print("Step size:", step)
# Output:
# Array 3: [ 0.   2.5  5.   7.5 10. ]
# Step size: 2.5
```

**Explanation:**

* Generates **`num_points` evenly spaced numbers** between `start` and `stop`.
* `endpoint=True` → includes the stop value; `False` → excludes it.
* `retstep=True` → also returns the **step size**.
* Unlike `np.arange`, which uses a fixed **step**, `linspace` divides the interval into **equal parts**.
* Useful in AI/ML for **feature ranges, plotting, or generating continuous input sequences**.

**Quick Comparison: `np.arange` vs `np.linspace`**

| Function                        | How it works                                                                        | Use case                             |
| ------------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------ |
| `np.arange(start, stop, step)`  | Sequence with **fixed step size**, stop excluded                                    | When you know the step size          |
| `np.linspace(start, stop, num)` | Sequence with **specific number of evenly spaced values**, stop included by default | When you need exact number of points |

**Tip:**

* `arange` → discrete intervals
* `linspace` → continuous ranges, plotting, AI/ML input sequences

---

### **6. Using `np.eye(n)` – Identity Matrix**

* The `numpy.eye()` function creates an **identity matrix**, which is a square matrix with ones on the diagonal and zeros elsewhere.
* **Syntax:**

```python
numpy.eye(N, M=None, k=0, dtype=float, order='C')
```

**Parameters:**

* `N` → number of rows
* `M` → number of columns (optional, defaults to N)
* `k` → diagonal offset (0 for main diagonal, positive → above, negative → below)
* `dtype` → data type of elements
* `order` → memory layout (C or F)

**Example:**

```python
import numpy as np

# 3x3 identity matrix
id_mat = np.eye(3)
print(id_mat)
# Output:
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]

np.eye(3,3,1)
# Output: Offset by 1
array([[0., 1., 0.],
       [0., 0., 1.],
       [0., 0., 0.]])
```

**Explanation:**

* Identity matrix → ones on the diagonal, zeros elsewhere.
* Useful in linear algebra.
* Can specify `k` to shift the diagonal.

---

### **7. Random Arrays**

NumPy gives us different ways to create random numbers.
Here are the **3 most common functions**:

---

#### 7.1. **Uniform Random Numbers (`rand`)**

* Generates random numbers **uniformly** between 0 and 1: `[0.0, 1.0)`.
* Every number in this range has an **equal probability** of appearing.

```python
np.random.rand(5)      # 5 random numbers between 0 and 1
# Example: array([0.98229518, 0.40535033, 0.9270507 , 0.71793652, 0.36953476])
 Mean:  3.40216749/5= 0.680433498

np.random.rand(2,3)    # 2x3 matrix
# Example:
array([[0.57336031, 0.32508759, 0.14469693],
       [0.17932754, 0.64208865, 0.28887194]])
```

👉 Use when you want **fair random numbers** in \[0,1].
---

#### 7.2. **Standard Normal Distribution (`randn`)**

* * Generates random numbers from a **standard normal (Gaussian) distribution**.
* Mean = 0, Standard deviation = 1.
* Numbers closer to 0 are **more likely**, and numbers farther from 0 are **less likely**.
* Because the distribution includes both positive and negative numbers, the average (mean) of a large number of generated numbers tends to hover around 0.
* The negative numbers balance out the positive numbers, so when you calculate the average, it comes close to 0.
* Mean = 0, Standard Deviation = 1.
  - The mean is the "center" of the data.
  - The standard deviation (std) measures how spread out the numbers are from the mean.
    - Small std → values are close to mean.
    - Large std → values are more spread out.
    - std = 0 → no spread (all numbers are the same)
    - std > 0 → there is spread (numbers differ from the mean)
* Some numbers will be negative.

```python
np.random.randn(5)     # 5 numbers from standard normal
# Example: array([ 0.78889004,  1.40283174, -0.76172686, -0.58904814,  0.17117123])
mean: 0.20

- If you generate a very large number of samples, the mean will get closer to 0.
- For small arrays, like your 5 numbers, the mean can be slightly positive or negative, depending on the random values.

1. Dataset A: `[6, 6, 6, 6, 6]`

   * Mean = 6
   * All values = mean → **std = 0**

2. Dataset B: `[1, 11, 6, 0, 12]`

   * Mean = 6
   * Values differ from mean → **std > 0**
   * Actual std (calculated using NumPy):

     ```python
     import numpy as np
     data = [1, 11, 6, 0, 12]
     np.std(data)  # Output: 5.0
     ```
   * So here, **std = 5**, which measures the spread.

✅ **Rule of thumb:**

* `std = 0` → no spread (all numbers are the same)
* `std > 0` → there is spread (numbers differ from the mean)
```

👉 Use when you want data that looks like **real-world variations** (e.g., heights, errors).

---

#### 7.3. **Random Integers (`randint`)**

* Generates **whole numbers** in a given range.
* The upper limit is **exclusive**.

```python
np.random.randint(1, 100, 10)   # 10 random integers from 1 to 99
# Example: array([45, 12, 89, 67, 23, 90, 11, 54, 72, 6])
```

👉 Use when you need **discrete values** (IDs, categories, counts).

---

## 🔑 Quick Comparison

| Function       | Range / Distribution   | Example Output        |
| -------------- | ---------------------- | --------------------- |
| `rand()`       | Uniform \[0,1)         | \[0.12, 0.88, 0.56]   |
| `randn()`      | Normal (mean=0, std=1) | \[0.34, -1.21, 0.88]  |
| `randint(a,b)` | Integers in \[a, b)    | \[45, 12, 89, 67, 23] |

---

## 💡 Why Important in AI/ML?

* **`rand()`** → Weight initialization in neural networks.
* **`randn()`** → Simulating noisy real-world data.
* **`randint()`** → Creating labels, IDs, or randomized experiments.

---

### **8. Array Attributes**

* Arrays have properties that tell you about their **size, shape, and type**.

**Explanation:**

#### 8.1 `.reshape` → The numpy.reshape() function allows for changing the shape of a NumPy array without altering its underlying data. This is a fundamental operation in data manipulation
  - To give a new shape to an existing array. The shape defines the number of elements along each dimension.
  - A new array object with the specified shape. The original array remains unchanged.
  - The data elements of the original array are maintained in the new array, just rearranged according to the new shape.
  - The total number of elements in the new shape must be the same as the total number of elements in the original array.
**Example:**

```python
randarr = np.random.randint(0,1000,8)
print(randarr)
Output: [399 299 797 685 176 594  22 749]

randarr.reshape(4,2)
Output: array([[399, 299],
       [797, 685],
       [176, 594],
       [ 22, 749]], dtype=int32)
```
#### 8.2 `.max()`, `.min()`, `.argmax()`, `.argmin()` → Find values and their locations

* `.max()` → Returns the **maximum value** in the array.
* `.min()` → Returns the **minimum value** in the array.
* `.argmax()` → Returns the **index of the maximum value**.
* `.argmin()` → Returns the **index of the minimum value**.
* * `.shape` → Returns the **dimensions** of the array.
* `.dtype` → Returns the **data type** of the array elements.


Example: (rows, columns) for 2D arrays, (length,) for 1D arrays.

8.3 .dtype → Returns the data type of the array elements.

Example: int32, float64, etc.

**Example:**

```python
arr = np.array([10, 23, 49, 5, 17])

print("Array:", arr)
print("Max value:", arr.max())        # Output: 49
print("Min value:", arr.min())        # Output: 5
print("Index of max value:", arr.argmax())  # Output: 2
print("Index of min value:", arr.argmin())  # Output: 3
```

---

### **9. Array Methods**

**Common Methods:**

```python
arr = np.array([1, 2, 3, 4, 5])

# Reshape 1D → 2D column vector
arr2d = arr.reshape((5,1))
print(arr2d)
# Output: [[1]
#          [2]
#          [3]
#          [4]
#          [5]]

# Find max/min and their indices
print(arr.max())      # 5
print(arr.min())      # 1
print(arr.argmax())   # 4
print(arr.argmin())   # 0
print(arr2d.shape)   # (5, 1)
print(arr.shape)     # (5,)
print(arr2d.dtype)    # int64
```

**Explanation:**

* `reshape(new_shape)` → changes shape without altering data
* `max()` / `min()` → largest/smallest value
* `argmax()` / `argmin()` → position of largest/smallest value
* Essential for **data preprocessing and feature analysis**

---

### **10. Vectorized Operations**

* NumPy supports **element-wise operations** without loops, which is critical for AI/ML.

**Example:**

```python
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

z = x + y
print(z)  # Output: [5 7 9]

z = x * y
print(z)  # Output: [4 10 18]
```

**Explanation:**

* Arithmetic operations are applied **to each element individually**.
* Avoids Python loops → much faster for large arrays.
* Works for **vectors, matrices, and higher-dimensional tensors**.

---

✅ **Tips for Beginners:**

* Always check `.shape` and `.dtype` before using arrays in ML models.
* Prefer NumPy vectorized operations over Python loops for **speed and efficiency**.
* Combine attributes, methods, and random arrays to **prepare datasets and initialize weights** efficiently.
