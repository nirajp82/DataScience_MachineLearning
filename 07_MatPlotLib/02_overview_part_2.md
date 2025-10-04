# Matplotlib Part 2: Object-Oriented Plotting

---
## 1\. `plt.subplots` vs. `figure.add_axes`

Both methods create **Axes** (the plotting area), but they differ entirely in their purpose and how they position the plot within the **Figure** (the overall container).

| Feature | plt.subplots() | figure.add_axes([left, bottom, width, height]) |
| :--- | :--- | :--- |
| **Purpose** | Creates a **Figure** and one or more subplots in a regular **grid**. | Adds an **Axes** at a specific, custom location in an **existing Figure**. |
| **Returns** | A tuple: `(Figure, Axes or array of Axes)` | The **Axes** object only. |
| **Layout** | **Automatic grid layout** (standard rows/columns), handling spacing for you. | **Manual positioning** using normalized coordinates (0 to 1). |
| **Use Case** | Standard single plots, comparing datasets side-by-side in a grid. | **Inset plots**, non-standard arrangements, or when exact placement is needed. |

### Example: Using `plt.subplots` (Standard Grid)

This is the recommended approach for most standard plotting tasks.

```python
import matplotlib.pyplot as plt

# Creates a Figure and a 1-row, 2-column array of Axes
fig, axes = plt.subplots(nrows=1, ncols=2)

axes[0].plot([1, 2, 3], [4, 5, 6])
axes[1].plot([1, 2, 3], [6, 5, 4])

# Adjusts spacing to prevent titles and labels from overlapping
plt.tight_layout() 
```

### Example: Using `figure.add_axes` (Custom Inset)

Coordinates `[left, bottom, width, height]` are relative to the figure, where `0.0` is the bottom/left and `1.0` is the top/right.

```python
import matplotlib.pyplot as plt

fig = plt.figure()

# Main Axes: covers most of the figure space (0.1 to 0.9 on each axis)
ax1 = fig.add_axes([0.1, 0.1, 0.8, 0.8]) 
ax1.plot([1, 2, 3], [4, 5, 6], label="Main")

# Inset Axes: manually placed within the top-right corner of the main plot
ax2 = fig.add_axes([0.65, 0.65, 0.2, 0.2]) 
ax2.plot([1, 2, 3], [6, 5, 4], color='red', label="Inset")

ax1.legend()
```

✅ **Tip:** Use **`plt.subplots`** for most standard plots; reserve **`add_axes`** for advanced layouts, like creating the inset plot above.

-----

## 2\. Creating Subplots

### Single Subplot

```python
fig, axes = plt.subplots()
axes.plot(x, y)
```

### Multiple Subplots

Always specify the number of rows and columns:

```python
# Creates a 1-row, 2-column arrangement
fig, axes = plt.subplots(nrows=1, ncols=2)

# Create a 3x3 grid of subplots
fig, axes = plt.subplots(nrows=3, ncols=3)
plt.tight_layout()
```

-----

## 3\. Working with Axes Array

When creating multiple subplots, the `axes` object returned is a **NumPy array**. You must index or iterate over this array to target individual plots.

```python
# fig is the Figure, axes is the 1D array of Axes
fig, axes = plt.subplots(nrows=1, ncols=2)

# Index axes
axes[0].plot(x, y)
axes[1].plot(y, x)

# Set titles
axes[0].set_title('First Plot')
axes[1].set_title('Second Plot')

# Iterate through axes (useful for applying the same style to all)
for current_ax in axes:
    current_ax.grid(True)
```

-----

## 4\. Controlling Figure Size and DPI

Use the `figsize` (width, height in inches) and `dpi` (resolution) arguments to control the output size and quality.

### Using `figure` and `add_axes`

```python
fig = plt.figure(figsize=(3, 2), dpi=100)
# A simple fill-the-figure example
ax = fig.add_axes([0, 0, 1, 1]) 
ax.plot(x, y)
```

### Using `subplots`

```python
fig, axes = plt.subplots(figsize=(8, 2), nrows=2, ncols=1)
axes[0].plot(x, y)
axes[1].plot(y, x)
plt.tight_layout()
```

-----

## 5\. Saving Figures

Save the figure directly from the Figure object (`fig`).

```python
# Saves figure as a PNG file
fig.savefig('my_picture.png')

# Saves figure with high resolution (DPI)
fig.savefig('my_picture.pdf', dpi=300)
```

-----

## 6\. Adding Titles, Labels, and Legends

In the object-oriented approach, these methods are called on the **Axes** object (`ax`).

### Titles and Labels

```python
ax.set_title('My Plot Title')
ax.set_xlabel('X Label')
ax.set_ylabel('Y Label')
```

### Legends

Legends require setting a `label` in the plot call, then calling `ax.legend()`.

```python
ax.plot(x, x**2, label='x squared')
ax.plot(x, x**3, label='x cubed')
ax.legend()
```

### Customizing Legend Location

```python
ax.legend(loc=0)            # Automatic best location
ax.legend(loc=10)           # Location code (e.g., 'center')
ax.legend(loc=(0.1, 0.1))   # Custom position using normalized coordinates
```

-----

## 7\. Key Takeaways

  * **`plt.subplots`** creates axes in a grid layout, easy to manage multiple plots.
  * **`figure.add_axes`** allows manual positioning, useful for insets or custom layouts.
  * **Axes arrays** can be indexed or iterated for multiple plots.
  * **Figure size** and **DPI** control output dimensions and resolution.
  * **Legends and labels** are customized via `ax.set_*` methods.
