# 🧾 NumPy Cheatsheet
---

## 📌 Tuple vs Arguments (Cheat Box)

* **Use a tuple** when specifying an **array shape**: `(rows, cols, ...)`
  Examples: `np.zeros((2,3))`, `np.ones((3,3))`, `np.full((2,2), 7)`.
* **Use separate arguments** when specifying **sequence / range parameters**: `start, stop, step` or `start, stop, num_points`
  Examples: `np.arange(0, 10, 2)`, `np.linspace(0, 1, 5)`.

## **NumPy functions table**:
```python
| Function              | Example / Code                  | Type | Produces 1D? | Produces 2D? | Output                                                                      |
| --------------------- | ------------------------------- | ------- | ----------- | ----------- | --------------------------------------------------------------------------- |
| `np.arange()`         | `np.arange(6)`                  | 1D      | ✅           | ❌           | `[0 1 2 3 4 5]`                                                             |
| `np.arange()`         | `np.arange(6).reshape(2,3)`     | 1D      | ✅           | ✅ (reshape) | `[[0 1 2][3 4 5]]`                                                          |
| `np.linspace()`       | `np.linspace(0,1,5)`            | 1D      | ✅           | ❌           | `[0. 0.25 0.5 0.75 1.]`                                                     |
| `np.logspace()`       | `np.logspace(0,2,5)`            | 1D      | ✅           | ❌           | `[1. 3.16227766 10. 31.6227766 100.]`                                       |
| `np.zeros()`          | `np.zeros(3)`                   | 2D      | ✅           | ✅           | `[0. 0. 0.]`                                                                |
| `np.zeros()`          | `np.zeros((2,3))`               | 2D      | ✅           | ✅           | `[[0. 0. 0.][0. 0. 0.]]`                                                    |
| `np.ones()`           | `np.ones(4)`                    | 2D      | ✅           | ✅           | `[1. 1. 1. 1.]`                                                             |
| `np.ones()`           | `np.ones((2,2))`                | 2D      | ✅           | ✅           | `[[1. 1.][1. 1.]]`                                                          |
| `np.full()`           | `np.full(3,7)`                  | 2D      | ✅           | ✅           | `[7 7 7]`                                                                   |
| `np.full()`           | `np.full((2,3),7)`              | 2D      | ✅           | ✅           | `[[7 7 7][7 7 7]]`                                                          |
| `np.eye()`            | `np.eye(3)`                     | 2D      | ❌           | ✅           | `[[1. 0. 0.][0. 1. 0.][0. 0. 1.]]`                                          |
| `np.identity()`       | `np.identity(2)`                | 2D      | ❌           | ✅           | `[[1. 0.][0. 1.]]`                                                          |
| `np.array()`          | `np.array([1,2,3])`             | 1D      | ✅           | ✅           | `[1 2 3]`                                                                   |
| `np.array()`          | `np.array([[1,2,3],[4,5,6]])`   | 1D      | ✅           | ✅           | `[[1 2 3][4 5 6]]`                                                          |
| `np.random.rand()`    | `np.random.rand(3)`             | 1D      | ✅           | ✅ (reshape) | `[0.5488135 0.71518937 0.60276338]`                                         |
| `np.random.rand()`    | `np.random.rand(2,3)`           | 2D      | ❌           | ✅           | `[[0.54488318 0.4236548 0.64589411][0.43758721 0.891773 0.96366276]]`       |
| `np.random.randn()`   | `np.random.randn(3)`            | 1D      | ✅           | ✅ (reshape) | `[0.24196227 -1.91328024 -1.72491783]`                                      |
| `np.random.randn()`   | `np.random.randn(2,3)`          | 2D      | ❌           | ✅           | `[[-0.56228753 -1.01283112 0.31424733][-0.90802408 -1.4123037 1.46564877]]` |
| `np.random.randint()` | `np.random.randint(0,10,3)`     | 1D      | ✅           | ✅ (reshape) | `[5 0 3]`                                                                   |
| `np.random.randint()` | `np.random.randint(0,10,(2,3))` | 2D      | ❌           | ✅           | `[[7 9 3][5 2 4]]`                                                          |
| `np.empty()`          | `np.empty(3)`                   | 1D      | ✅           | ✅ (reshape) | `[2.0e-322 0.0 1.0e-323]` (garbage values)                                  |
| `np.tile()`           | `np.tile([1,2],2)`              | 1D      | ✅           | ✅ (reshape) | `[1 2 1 2]`                                                                 |
| `np.repeat()`         | `np.repeat([1,2],3)`            | 1D      | ✅           | ✅ (reshape) | `[1 1 1 2 2 2]`                                                             |
| `np.meshgrid()`       | `np.meshgrid([1,2],[3,4])`      | 2D      | ❌           | ✅           | `[[1 2][1 2]] [[3 3][4 4]]`                                                 |

```
---

## 0. Creating Arrays — 1D & 2D (with input → output)

```python
import numpy as np

arr1d = np.array([10, 20, 30, 40])
print(arr1d)
# Output: [10 20 30 40]

arr2d = np.array([[1, 2, 3],
                  [4, 5, 6]])
print(arr2d)
# Output:
# [[1 2 3]
#  [4 5 6]]
```

### Zeros, Ones, Full, Eye, Identity, Arange, Linspace

```python
np.zeros((2,3))
# Output:
# [[0. 0. 0.]
#  [0. 0. 0.]]

np.ones((3,3))
# Output:
# [[1. 1. 1.]
#  [1. 1. 1.]
#  [1. 1. 1.]]

np.full((2,2), 7)
# Output:
# [[7 7]
#  [7 7]]

np.eye(3)
# Output:
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]

np.identity(3)
# Output:
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]

np.arange(0, 10, 2)
# Output: [0 2 4 6 8]

np.linspace(0, 1, 5)
# Output: [0.   0.25 0.5  0.75 1. ]
```

**Note:** `np.eye` is more flexible (see notes below); `np.identity(n)` is a convenience wrapper for the common square-case.

---

## `_like` Functions & dtypes (examples)

```python
arr = np.array([[1,2],[3,4]], dtype=np.int32)
print(arr.dtype)
# Output: int32

np.zeros_like(arr)
# Output:
# [[0 0]
#  [0 0]]

np.ones_like(arr)
# Output:
# [[1 1]
#  [1 1]]

np.array([1,2,3], dtype=float)
# Output: [1. 2. 3.]

np.zeros(5, dtype='int32')
# Output: [0 0 0 0 0]
```

---

## 1. Array Attributes

```python
arr2d.shape    # Output: (2, 3)
arr2d.ndim     # Output: 2
arr2d.size     # Output: 6
arr2d.dtype    # Output: dtype('int64')  # depends on system
arr2d.T
# Output:
# [[1 4]
#  [2 5]
#  [3 6]]
```

---

## 2. Indexing & Slicing

```python
arr2d[0, 1]    # Output: 2
arr2d[:, 1]    # Output: [2 5]
arr2d[1, :]    # Output: [4 5 6]
arr1d[1:3]     # Output: [20 30]
arr1d[::2]     # Output: [10 30]
```

---

## 3. Reshape, Flattening, Views — `reshape`, `ravel`, `flatten`

### Reshape

```python
np.arange(6).reshape(2,3)
# Output:
# [[0 1 2]
#  [3 4 5]]
```

### `ravel()` vs `flatten()` — important difference

```python
arr3 = np.array([[1,2,3],[4,5,6]])
r = arr3.ravel()     # view when possible
f = arr3.flatten()   # always copy

print("ravel:", r)   # Output: [1 2 3 4 5 6]
print("flatten:", f) # Output: [1 2 3 4 5 6]

# If you modify the ravel() result (a view), the original changes:
r[0] = 99
print(arr3)
# Output:
# [[99  2  3]
#  [ 4  5  6]]

# If you modify the flatten() result (a copy), the original stays the same:
arr4 = np.array([[1,2,3],[4,5,6]])
f2 = arr4.flatten()
f2[0] = 88
print(arr4)
# Output:
# [[1 2 3]
#  [4 5 6]]
print("flatten copy modified:", f2)
# Output: [88  2  3  4  5  6]
```

**Rule:** `ravel()` → view when possible (fast, memory efficient). `flatten()` → copy (safer when you need to modify without affecting the original).

---

## 4. Stacking & Concatenation (`hstack`, `vstack`, `stack`, `concatenate`)

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

np.hstack([a,b])
# Output: [1 2 3 4 5 6]

np.vstack([a,b])
# Output:
# [[1 2 3]
#  [4 5 6]]

np.stack([a,b])
# Output:
# [[1 2 3]
#  [4 5 6]]

np.concatenate([a,b])
# Output: [1 2 3 4 5 6]

# stack with new axis:
np.stack([a,b], axis=1)
# Output:
# [[1 4]
#  [2 5]
#  [3 6]]
```

**Note:**

* `hstack`/`vstack` concatenate along an *existing* axis.
* `stack` creates a **new axis** (shape changes differently).
* `concatenate` joins along the axis you specify.

---

## 5. Math Operations, Matrix Mult, Reductions

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

a + b        # Output: [5 7 9]
a * b        # Output: [ 4 10 18]
np.dot(a,b)  # Output: 32

A = np.array([[1,2],[3,4]])
B = np.array([[5,6],[7,8]])
A @ B
# Output:
# [[19 22]
#  [43 50]]

arr2d = np.array([[1,2,3],[4,5,6]])
np.sum(arr2d)            # Output: 21
np.sum(arr2d, axis=0)    # Output: [5 7 9]
np.sum(arr2d, axis=1)    # Output: [ 6 15]
np.prod(arr2d)           # Output: 720
```

### Universal functions (ufuncs)

```python
arr = np.array([1., 4., 9.])
np.sqrt(arr)   # Output: [1. 2. 3.]
np.exp(arr)    # Output: [2.718282 54.59815 8103.083928]
np.log(arr)    # Output: [0.      1.386294 2.197225]
```

---

## 6. Statistics

```python
arr = np.array([1,2,3,4,5])
np.mean(arr)    # Output: 3.0
np.median(arr)  # Output: 3.0
np.std(arr)     # Output: 1.4142135623730951
np.var(arr)     # Output: 2.0
np.min(arr)     # Output: 1
np.max(arr)     # Output: 5
np.argmax(arr)  # Output: 4
np.argmin(arr)  # Output: 0
```

---

## 7. Random (seeded examples — deterministic)

```python
np.random.seed(42)
np.random.rand(2,3)
# Example Output:
# [[0.37454 0.950714 0.731994]
#  [0.598658 0.156019 0.155995]]

np.random.seed(42)
np.random.randn(2,3)
# Example Output:
# [[ 0.496714 -0.138264  0.647689]
#  [ 1.52303  -0.234153 -0.234137]]

np.random.seed(42)
np.random.randint(0,10,(2,2))
# Example Output:
# [[6 9]
#  [2 6]]

np.random.seed(42)
np.random.choice([1,2,3], 5)
# Example Output: [2 3 1 1 2]
```

---

## 8. Boolean & Filtering

```python
arr = np.array([3,7,1,9,5])

arr > 5                    # Output: [False  True False  True False]
arr[arr > 5]               # Output: [7 9]
np.where(arr > 5, 1, 0)    # Output: [0 1 0 1 0]
np.any(arr > 8)            # Output: True
np.all(arr > 0)            # Output: True
```

---

## 9. Useful Utilities (`unique`, `sort`, `argsort`, `copy`, `delete`, `insert`)

```python
arr = np.array([3,1,2,2,3,1])

np.unique(arr)     # Output: [1 2 3]
np.sort(arr)       # Output: [1 1 2 2 3 3]
np.argsort(arr)    # Output: [1 5 2 3 0 4]

arrx = np.array([3,1,2])
np.copy(arrx)             # Output: [3 1 2]
np.delete(arrx, 0)        # Output: [1 2]
np.insert(arrx, 1, 99)    # Output: [ 3 99  1  2]
```

---

## 10. Copy vs View — be explicit

```python
orig = np.array([1,2,3])
view = orig.view()
copy = orig.copy()

view[0] = 9
copy[1] = 88

print("orig after view[0]=9:", orig)
# Output: [9 2 3]

print("view:", view)
# Output: [9 2 3]

print("copy (modified):", copy)
# Output: [ 1 88  3]
```

**Rule:** `view()` returns a new array object that **shares** the same memory (changing it updates original). `copy()` returns an independent copy.

---

## 11. Linear Algebra

```python
A = np.array([[1.,2.],[3.,4.]])
np.linalg.inv(A)
# Output:
# [[-2.   1.  ]
#  [ 1.5 -0.5]]

np.linalg.det(A)
# Output: -2.0

vals, vecs = np.linalg.eig(A)
# Example Output:
# vals -> [-0.37228132  5.37228132]
# vecs ->
# [[-0.82456484 -0.41597356]
#  [ 0.56576746 -0.90937671]]

B = np.array([[1,2],[3,5]], dtype=float)
b = np.array([1,2], dtype=float)
np.linalg.solve(B, b)   # Output: [-1.  1.]
```

---

## 12. `eye` vs `identity` — what’s different?

* `np.eye(N, M=None, k=0, dtype=float)`

  * Can create **rectangular** arrays (different #columns), and `k` shifts the diagonal (k>0 shifts right, k<0 shifts left).
  * Example:

    ```python
    np.eye(3, 4, k=1)
    # Output:
    # [[0. 1. 0. 0.]
    #  [0. 0. 1. 0.]
    #  [0. 0. 0. 1.]]
    ```
* `np.identity(N, dtype=None)`

  * Convenience wrapper for `np.eye(N)` when you only want a square identity matrix.
  * `np.array_equal(np.eye(3), np.identity(3))` → `True`.

**Rule:** Use `np.identity` for the simple square identity; use `np.eye` when you need control (rectangular, diagonal offset `k`, dtype, etc.).

---

## 13. `arange` vs `linspace`

* `np.arange(start, stop, step)` — like Python's `range`, uses `step`. Good when step size is known. always produces 1D array.

  * Example: `np.arange(0,10,2) -> [0 2 4 6 8]`
* `np.linspace(start, stop, num)` — specify the **number of points** you want evenly spaced from `start` to `stop` (inclusive by default).

  * Example: `np.linspace(0,1,5) -> [0.   0.25 0.5  0.75 1. ]`

---

## 14. Quick Memory/Practical Tips (short checklist)

* If you want to **change shape** → pass a **tuple**: `np.zeros((rows, cols))`.
* If you want to **generate numbers** → pass **separate args**: `np.arange(start, stop, step)`.
* Want to **modify** a flattened array and keep original safe? Use `.flatten()` (copy).
  Want a memory-efficient flatten that may modify original? Use `.ravel()` (view when possible).
* Need an **independent copy** before mutating? Use `.copy()`.
* Need a **square identity** → `np.identity(n)`; need extra control → `np.eye`.
* Use `np.stack` to add a new axis; use `hstack/vstack/concatenate` to join along existing axes.
* For deterministic random results: call `np.random.seed(...)` before generating random numbers.

---

## 15. Final Notes & Suggested Practice

* These minor differences matter often in debugging (unexpected in-place changes or memory use). When in doubt, prefer **explicit** calls:

  * `x.copy()` when you need isolation.
  * `np.eye` with `k` when you need an offset diagonal.
  * `np.stack(..., axis=...)` when you want exact axis semantics.
* Keep a tiny test script (like the one I used to capture these outputs) to quickly confirm behavior in your local NumPy version — semantics are stable but exact printed formatting / dtype defaults may vary by platform.

---
