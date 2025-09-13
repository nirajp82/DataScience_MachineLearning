# **NumPy Arrays: Examples Explained for Beginners**

---

## **Table of Contents**

1. [Creating Arrays from Python Lists](#1-creating-arrays-from-python-lists)  
2. [Using `np.arange(start, stop, step)`](#2-using-nparangestart-stop-step)  
3. [Using `np.zeros(shape)`](#3-using-npzerosshape)  
4. [Using `np.ones(shape)`](#4-using-nponesshape)  
5. [`np.linspace(start, stop, num_points)`](#5-nplinspace-start-stop-num_points)  
6. [Using `np.eye(n)`](#6-using-npeyn)  
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

### **5. `np.linspace(start, stop, num_points)`**

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

### **6. Using `np.eye(n)`**

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
```

**Explanation:**

* Identity matrix → ones on the diagonal, zeros elsewhere.
* Useful in linear algebra.
* Can specify `k` to shift the diagonal.

---

### **7. Random Arrays**

**Uniform Random Numbers:**

```python
np.random.rand(4)      # 1D array, 4 random numbers between 0 and 1
np.random.rand(3,3)    # 3x3 matrix of random numbers between 0 and 1
```

**Standard Normal Distribution:**

```python
np.random.randn(5)     # 1D array of 5 numbers from standard normal (mean=0, std=1)
```

**Random Integers:**

```python
np.random.randint(1, 100, 10)  # 10 random integers from 1 to 99
```

**Explanation:**

* `rand()` → uniform distribution (0–1)
* `randn()` → Gaussian distribution (mean=0, std=1)
* `randint(low, high, size)` → random integers in \[low, high)
* Essential in AI/ML for **weight initialization, simulations, or creating random datasets**

---

### **8. Array Attributes**

* Arrays have properties that tell you about their **size, shape, and type**.

**Example:**

```python
arr = np.array([[1,2,3],[4,5,6]])

arr.shape   # Output: (2, 3)
arr.size    # Output: 6
arr.dtype   # Output: int64
```

**Explanation:**

* `.shape` → dimensions of the array (rows × columns)
* `.size` → total number of elements (2×3 = 6)
* `.dtype` → data type of elements (int, float, etc.)
* Always useful to check before feeding data into ML models.

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
