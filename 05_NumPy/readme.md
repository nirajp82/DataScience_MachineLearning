# NumPy Cheatsheet

### 0\. Creating Arrays

A NumPy array is a grid of values, all of the same type.

**1D Array**

```python
import numpy as np

arr1d = np.array([10, 20, 30, 40])
print(arr1d)
# Output: [10 20 30 40]
```

**2D Array**

```python
arr2d = np.array([[1, 2, 3],
                  [4, 5, 6]])
print(arr2d)
# Output:
# [[1 2 3]
#  [4 5 6]]
```

**Common Creation Functions**

```python
np.zeros((2,3))      # [[0. 0. 0.]
                     #  [0. 0. 0.]]

np.ones((3,3))       # [[1. 1. 1.]
                     #  [1. 1. 1.]
                     #  [1. 1. 1.]]

np.full((2,2), 7)    # [[7 7]
                     #  [7 7]]

np.eye(3)            # [[1. 0. 0.]
                     #  [0. 1. 0.]
                     #  [0. 0. 1.]]

np.arange(0, 10, 2)  # [0 2 4 6 8]

np.linspace(0, 1, 5) # [0.   0.25 0.5  0.75 1. ]

np.zeros_like(arr2d) # Creates a zeros array with the same shape as arr2d

np.array([1, 2, 3], dtype='float') # Creates array with specified data type
```

### 1\. Array Attributes

These properties provide information about the array's structure.

```python
arr2d.shape   # (2, 3) - Dimensions of the array
arr2d.ndim    # 2      - Number of dimensions
arr2d.size    # 6      - Total number of elements
arr2d.dtype   # int64  - Data type of the elements
arr2d.T       # Transpose of the array
```

### 2\. Indexing & Slicing

Accessing and selecting parts of an array.

```python
arr2d[0, 1]     # 2        (row 0, col 1)
arr2d[:, 1]     # [2 5]    (all rows, 2nd column)
arr2d[1, :]     # [4 5 6]  (2nd row)
arr1d[1:3]      # [20 30]  (elements from index 1 up to 3)
arr1d[::2]      # [10 30]  (every other element)
```

### 3\. Reshape & Stacking

Changing an array's shape or combining multiple arrays.

```python
# Reshaping
np.arange(6).reshape(2,3)
# [[0 1 2]
#  [3 4 5]]

# Flattening
arr2d.flatten() # Returns a new, flattened array: [1 2 3 4 5 6]
arr2d.ravel()   # Returns a view of the flattened array (more memory efficient)

# Stacking
np.hstack([arr1d, arr1d]) # Horizontal stack
# [10 20 30 40 10 20 30 40]

np.vstack([arr1d, arr1d]) # Vertical stack
# [[10 20 30 40]
#  [10 20 30 40]]

np.stack([arr1d, arr1d])  # Stacks along a new axis
# [[10 20 30 40]
#  [10 20 30 40]]
```

### 4\. Math Operations

NumPy's math operations are fast and apply element-wise.

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

a + b       # [5 7 9]  (element-wise addition)
a * b       # [ 4 10 18] (element-wise multiplication)
a ** 2      # [1 4 9]

np.dot(a,b)   # 32  (dot product of two vectors)
a @ b         # 32  (same as np.dot)

# Universal Functions (Ufuncs)
np.exp(a)     # [2.718... 7.389... 20.085...]
np.sqrt(a)    # [1.         1.41421356 1.73205081]
```

**Reduction Operations with `axis`**
These functions compute a single value along an axis.

```python
arr2d = np.array([[1, 2, 3], [4, 5, 6]])
np.sum(arr2d)          # 21  (sum of all elements)
np.sum(arr2d, axis=0)  # [5 7 9]  (sum of each column)
np.sum(arr2d, axis=1)  # [6 15]   (sum of each row)
```

### 5\. Statistics

Common statistical functions for analysis.

```python
arr = np.array([1,2,3,4,5])

np.mean(arr)   # 3.0
np.median(arr) # 3.0
np.std(arr)    # 1.414
np.min(arr)    # 1
np.max(arr)    # 5
np.argmax(arr) # 4 (index of the max value)
np.argmin(arr) # 0 (index of the min value)
```

### 6\. Random

Generating random numbers and arrays.

```python
np.random.rand(2,3)          # Uniform distribution [0, 1)
np.random.randn(2,3)         # Standard normal distribution
np.random.randint(0,10,(2,2))# Random integers [0, 10)
np.random.choice([1,2,3], 5) # Random picks with replacement
np.random.seed(42)           # Fixes the randomness for reproducibility
```

### 7\. Boolean & Filtering

Selecting elements based on a condition.

```python
arr = np.array([3,7,1,9,5])

arr[arr > 5]            # [7 9]        (boolean indexing)
np.where(arr > 5, 1, 0)   # [0 1 0 1 0]  (replace values based on condition)
np.any(arr > 8)         # True
np.all(arr > 0)         # True
```

### 8\. Useful Utilities

Miscellaneous functions for array manipulation and file I/O.

```python
arr = np.array([3,1,2,2,3,1])

np.unique(arr)      # [1 2 3]
np.sort(arr)        # [1 1 2 2 3 3]
np.argsort(arr)     # [1 5 2 3 0 4] (returns indices that would sort the array)

np.concatenate([arr, arr]) # [3 1 2 2 3 1 3 1 2 2 3 1]

# File I/O
np.save('my_array.npy', arr) # Save a NumPy array to a binary file
np.load('my_array.npy')      # Load the array back
```

### 9\. Linear Algebra

Powerful functions for matrix operations.

```python
A = np.array([[1,2],[3,4]])

np.linalg.inv(A)   # [[-2.   1. ]
                   #  [ 1.5 -0.5]] (inverse of a matrix)

np.linalg.det(A)   # -2.0  (determinant of a matrix)

# Solve a linear system Ax = b
b = np.array([1, 2])
np.linalg.solve(A, b) # [-1.  1.]
```
