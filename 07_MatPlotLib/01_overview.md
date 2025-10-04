# Introduction to Matplotlib (Part 1)

Matplotlib is a powerful Python library for creating static, animated, and interactive visualizations.  
This guide introduces the **basics of plotting with Matplotlib**, focusing on both the quick functional style and the more flexible object-oriented (OO) style.

---

## 🚀 Getting Started

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
x = np.linspace(0, 5, 11)
# Calculate the squared values
y = x ** 2
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

#### Multiple Plots on the Same Canvas

Use `plt.subplot(rows, cols, index)` to divide the figure into subplots.

```python
plt.subplot(1, 2, 1) # 1 row, 2 columns, first plot
plt.plot(x, y, 'r')  # 'r' = red line

plt.subplot(1, 2, 2) # 1 row, 2 columns, second plot
plt.plot(y, x, 'b')  # 'b' = blue line

plt.show()
```

---

### 2️⃣ Object-Oriented (OO) Approach

The OO method gives explicit control over figures and axes, which is essential for complex visualizations.

#### Creating a Figure and Axes

```python
fig = plt.figure()
# [left, bottom, width, height] are fractions of the figure size
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])
```

#### Plotting with OO Style

```python
ax.plot(x, y)

ax.set_xlabel('X Label')
ax.set_ylabel('Y Label')
ax.set_title('Title')
```

#### Multiple Axes in a Single Figure

This technique allows creating custom layouts, like inset plots:

```python
fig = plt.figure()

# Main axes
ax1 = fig.add_axes([0.1, 0.1, 0.8, 0.8])
# Inset axes
ax2 = fig.add_axes([0.2, 0.5, 0.4, 0.3])

ax1.plot(x, y)
ax2.plot(y, x)

ax1.set_title('Larger Plot')
ax2.set_title('Smaller Plot')

plt.show()
```

---

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

```
