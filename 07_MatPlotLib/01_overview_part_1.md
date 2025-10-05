## Introduction to Matplotlib (Part 1)

- Matplotlib is a powerful Python library for creating static, animated, and interactive visualizations.  
---

### Installation

Ensure you have **Matplotlib** and **NumPy** installed:

```bash
pip install matplotlib numpy
````

---

## 🛠️ Setup and Initial Imports

### Importing Matplotlib

The core of Matplotlib plotting is the `pyplot` module, typically imported as `plt`:

```python
import matplotlib.pyplot as plt
```

### Using Matplotlib in Jupyter Notebooks

To display plots directly within a Jupyter Notebook:

```python
%matplotlib inline
```

### Using Matplotlib in Python Scripts

If you are not in a Jupyter Notebook (for example, running a `.py` script), you must explicitly call:

```python
plt.show()
```

at the end of your plotting commands to render the visualization.

---

## 📊 Creating Basic Plots with NumPy

Plots are typically generated from data stored in **NumPy arrays**.

```python
import numpy as np

# Create data: 11 evenly spaced points between 0 and 5
x = np.linspace(0, 5, 11) //array([0., 0.5, 1., 1.5, 2., 2.5, 3., 3.5, 4., 4.5, 5. ])
# Calculate the squared values
y = x ** 2 //array([ 0., 0.25, 1., 2.25, 4., 6.25, 9., 12.25, 16., 20.25, 25.])

```
---

## 🖼️ Plotting Methods

Matplotlib provides two main ways to create plots:

1. **Functional (state-based) method** — quick and simple plotting.
2. **Object-Oriented (OO) method** — more control and customization.

---

### 1️⃣ Functional Plotting Method

This method uses global functions from `pyplot`.

#### Basic Plotting

```python
plt.plot(x, y)
plt.show()  # Required if not in a Jupyter Notebook
```

#### Adding Labels and Titles

```python
plt.xlabel('X Label')
plt.ylabel('Y Label')
plt.title('Title')
```
<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/84abfbb3-42b6-436f-9c44-aefb9d512af7" />

#### Multiple Plots on the Same Canvas

Use `plt.subplot(rows, cols, index)` to divide the figure into subplots.

`plt.subplot()` is used to place multiple plots (Axes) onto a single figure by organizing them into a **grid**.

### Syntax

```python
plt.subplot(R, C, P)
```

### Parameters

1. **R (Rows)** – number of horizontal divisions in the grid.

2. **C (Columns)** – number of vertical divisions in the grid.

   * **Rule:** All subplots in the same figure must use the same R and C values.

3. **P (Position)** – specifies the cell where the next plot will be drawn.

   * Counting starts at **1** from the **top-left corner**, proceeding **left-to-right** across rows.

### Example: 2×3 Grid

```
P=1   P=2   P=3
P=4   P=5   P=6
```

* `plt.subplot(2, 3, 1)` → top-left
* `plt.subplot(2, 3, 5)` → bottom-middle

### Key Points

* Enables **multiple plots in one figure**.
* Positions are **1-based** and **row-major order** (top-left → right → next row).
* Use **consistent R and C** values for all subplots in a figure.

```python
# The grid blueprint is set as 2 ROWS and 2 COLUMNS (2x2 grid)
# The R and C parameters (2 and 2) must remain the same for all subplots.
# 1. Select Position 1 (Top-Left)
# R=2, C=2, P=1 (Position 1)
plt.subplot(2, 2, 1) 
plt.plot(x, y, 'r')
plt.title('Position 1 (Top-Left)') 

# 2. Select Position 2 (Top-Right)
# R=2, C=2, P=2 (Position 2)
plt.subplot(2, 2, 2) 
plt.plot(y, x, 'b')
plt.title('Position 2 (Top-Right)') 

# 3. Select Position 3 (Bottom-Left)
# R=2, C=2, P=3 (Position 3)
plt.subplot(2, 2, 3) 
plt.plot(y, x, 'g')
plt.title('Position 3 (Bottom-Left)') 

# 4. Select Position 4 (Bottom-Right)
# R=2, C=2, P=4 (Position 4)
plt.subplot(2, 2, 4) 
plt.plot(x, y, 'k') # Changed to black ('k') for contrast
plt.title('Position 4 (Bottom-Right)') 

# Automatically adjusts subplot parameters for a tight layout
plt.tight_layout() 
plt.show()
```
<img width="300" height="150" alt="image" src="https://github.com/user-attachments/assets/4cfb9cfb-200a-465f-930c-8655cfd02875" />

---

### 2️⃣ Object-Oriented (OO) Approach

The OO method gives explicit control over figures and axes, which is essential for complex visualizations.

`fig.add_axes()` places an axes at an **exact position** inside a figure using **fractions of figure size**.

### Syntax

```python
ax = fig.add_axes([left, bottom, width, height])
```

### Parameters (fractions 0–1)

* **left** – horizontal start from figure left (0 = left edge, 1 = right edge).
* **bottom** – vertical start from figure bottom (0 = bottom edge, 1 = top edge).
* **width** – width of axes (fraction of figure width).
* **height** – height of axes (fraction of figure height).
  
#### Creating a Figure and Axes

```python
fig = plt.figure()
ax = fig.add_axes([0.1, 0.1, 0.3, 0.5])  # 10% from left, 50% from bottom, width 30%, height 50%
ax.plot(x, y)
ax.set_xlabel('X Label')
ax.set_ylabel('Y Label')
ax.set_title('Main Plot')
plt.show()
```
<img width="236" height="137" alt="image" src="https://github.com/user-attachments/assets/dbe235eb-b909-4ee8-a0a6-22b019eec8cb" />

#### Multiple Axes in a Single Figure

This technique allows creating custom layouts, like inset plots:

```python
fig = plt.figure()

# 1️: Main axes: large plot covering most of the figure
ax1 = fig.add_axes([0.1, 0.1, 0.8, 0.8])  # [left, bottom, width, height] as fractions
ax1.plot(x, y)
ax1.set_title('Main Plot')  # Clear title for the main plot

# 2️: Inset axes: smaller plot inside the main figure
ax2 = fig.add_axes([0.2, 0.5, 0.4, 0.3])  # Positioned 20% from left, 50% from bottom, width 40%, height 30%
ax2.plot(y, x)
ax2.set_title('Inset Plot 1') 

# 3: Additional inset axes: another small plot
ax3 = fig.add_axes([0.6, 0.2, 0.2, 0.2])  # Positioned 60% from left, 20% from bottom, width 20%, height 20%
ax3.plot(x, y)
ax3.set_title('Inset Plot 2') 

plt.show()
```
<img width="350" height="200" alt="image" src="https://github.com/user-attachments/assets/4420725c-024c-4186-9266-5b63855eaaa6" />
---

### Key Takeaways 

* Each `add_axes()` call creates a **new independent axes** on the figure.
* The `left, bottom, width, height` parameters **control absolute placement on the figure**, not relative to other axes.
* That’s why the **smaller plots appear “inside” the main plot** — their coordinates fall **within the same figure space**.
* You can add as many insets as you want; they **don’t split the main axes**, they just **overlay** on the figure.

## 📚 Summary

* **Figures and Axes:** Every plot lives inside a **Figure** (canvas) with one or more **Axes** (individual plots).
* **Functional vs. OO:**
  * Functional (`plt.plot`) → quick for simple plots.
  * OO (`fig`, `ax`) → best for complex layouts and fine control.
* **Subplots:** Use `plt.subplot()` (functional) or `fig.add_axes()` (OO) for multiple plots.
* **Customization:** Add labels, titles, and multiple axes for clear, flexible visualizations.

---

## 📝 Key Takeaways

* Install **Matplotlib + NumPy** to get started.
* Use `%matplotlib inline` for Jupyter, `plt.show()` for scripts.
* **Functional API** → quick plots.
* **OO API** → precise and customizable.
* Remember: `add_axes([left, bottom, width, height])` values are **fractions of figure size**, allowing you to position plots exactly where you want them.
