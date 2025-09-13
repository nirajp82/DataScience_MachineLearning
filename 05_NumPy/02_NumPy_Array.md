### **NumPy Arrays**

**1. What is a NumPy Array?**

* Main data structure in **NumPy** for storing elements efficiently.
* Can be **1D (vector)** or **2D (matrix)**.
* Used extensively in **AI/ML** for datasets, features, weights, and linear algebra operations.

**2. Creating Arrays:**

* **From Python lists:**

  ```python
  import numpy as np
  arr = np.array([1, 2, 3])          # 1D array
  mat = np.array([[1,2,3],[4,5,6]])  # 2D array
  ```
* **Using built-in NumPy functions:**

  * `np.arange(start, stop, step)` → evenly spaced values like Python’s range.
  * `np.zeros(shape)` → array of zeros.
  * `np.ones(shape)` → array of ones.
  * `np.linspace(start, stop, num_points)` → evenly spaced **floating-point numbers** over an interval.
  * `np.eye(n)` → identity matrix (useful in linear algebra).

**3. Random Arrays (Critical in AI/ML):**

* **Uniform distribution:** `np.random.rand(shape)` → values between 0 and 1.
* **Standard normal distribution (Gaussian):** `np.random.randn(shape)` → mean 0, std 1.
* **Random integers:** `np.random.randint(low, high, size)` → discrete random integers.

**4. Useful Array Attributes:**

* `arr.shape` → dimensions of array.
* `arr.dtype` → data type of elements (e.g., int32, float64).
* `arr.size` → total number of elements.

**5. Useful Array Methods:**

* `arr.reshape(new_shape)` → reshape array without changing data (total elements must match).
* `arr.max() / arr.min()` → maximum or minimum value.
* `arr.argmax() / arr.argmin()` → index of max/min value.
* Arithmetic operations are **element-wise**, ideal for vectorized AI/ML computations.

**6. Key Points for AI/ML:**

* Arrays are **faster and more memory-efficient** than Python lists.
* Used for **feature matrices, weights, biases, and dataset manipulation**.
* Reshaping and random number generation are essential for **data preprocessing, initialization of neural networks, and simulations**.
* Built-in functions like `zeros`, `ones`, `linspace`, and `eye` simplify **linear algebra operations**.

**7. Tips for Efficient Use:**

* Prefer **NumPy functions over Python loops** for performance.

## **NumPy Arrays - Cheat Sheet**

### **1. Import NumPy**

```python
import numpy as np
```

---

### **2. Creating Arrays**

**From Python lists:**

```python
arr = np.array([1, 2, 3])           # 1D array (vector)
mat = np.array([[1,2,3],[4,5,6]])  # 2D array (matrix)
```

**Using built-in functions:**

```python
np.arange(0, 10, 2)         # [0,2,4,6,8] → like Python range
np.zeros(5)                 # [0,0,0,0,0] → vector of zeros
np.zeros((2,3))             # 2x3 matrix of zeros
np.ones(4)                   # [1,1,1,1] → vector of ones
np.ones((3,2))              # 3x2 matrix of ones
np.linspace(0,5,10)         # 10 evenly spaced points from 0 to 5
np.eye(3)                   # 3x3 identity matrix
```

**Random Arrays (for AI/ML initialization & simulation):**

```python
np.random.rand(4)            # 1D array, uniform 0–1
np.random.rand(3,3)          # 3x3 matrix, uniform 0–1
np.random.randn(5)            # 1D array, standard normal (mean=0, std=1)
np.random.randint(1, 100, 10) # 10 random integers from 1 to 99
```

---

### **3. Array Attributes**

```python
arr.shape   # dimensions (rows, columns)
arr.size    # total number of elements
arr.dtype   # data type (int32, float64, etc.)
```

---

### **4. Array Methods**

```python
arr.reshape(new_shape)        # reshape array without changing data
arr.max()                     # maximum value
arr.min()                     # minimum value
arr.argmax()                  # index of max value
arr.argmin()                  # index of min value
```

---

### **5. Key Notes for AI/ML**

* **Arrays are faster & memory-efficient** than Python lists.
* **1D → vectors**, **2D → feature matrices**.
* Use **reshape** to match ML model input shapes.
* **Random numbers** are essential for initializing weights and data simulation.
* Always check **shape & dtype** before feeding data into models.
* Use **vectorized operations** instead of loops for performance.

* Always check **shape and dtype** before feeding arrays into ML models.
* Use **vectorized operations** instead of iteration for large datasets.

