# Matplotlib Part 3: Customizing Plot Appearance

---

## 🎨 Introduction

Matplotlib gives you full control over how your plots appear — from line colors to marker shapes, transparency, and axis limits. Customization allows you to create visually appealing and informative plots tailored to your needs.

---

## 📋 Customization Table

| **Feature**                  | **Parameter / Method** | **Description**                                                      | **Examples**                                                       |
| ---------------------------- | ---------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Color**                    | `color`                | Sets line color. Accepts named colors, RGB hex codes, or RGB tuples. | `'blue'`, `'orange'`, `'#f8c0a0'`, `(0.1, 0.2, 0.5)`               |
| **Line Width**               | `linewidth` or `lw`    | Controls line thickness.                                             | `lw=1` (default), `lw=2` (thicker), `lw=0.5` (thinner)             |
| **Transparency**             | `alpha`                | Controls opacity (0 = transparent, 1 = opaque).                      | `alpha=0.5` (semi-transparent)                                     |
| **Line Style**               | `linestyle` or `ls`    | Sets pattern of the line.                                            | `'-'` (solid), `'--'` (dashed), `'-. '` (dash-dot), `':'` (dotted) |
| **Markers**                  | `marker`               | Adds symbols for data points.                                        | `'o'` (circle), `'+'` (plus), `'*'` (star), `'x'` (cross)          |
| **Marker Size**              | `markersize` or `ms`   | Controls marker size.                                                | `ms=10` (larger markers)                                           |
| **Marker Fill Color**        | `markerfacecolor`      | Sets marker interior color.                                          | `markerfacecolor='yellow'`                                         |
| **Marker Edge Width**        | `markeredgewidth`      | Controls edge thickness of marker.                                   | `markeredgewidth=2`                                                |
| **Marker Edge Color**        | `markeredgecolor`      | Sets marker edge color.                                              | `markeredgecolor='black'`                                          |
| **X-axis Limits**            | `ax.set_xlim([a, b])`  | Defines visible range for X-axis.                                    | `ax.set_xlim([0, 1])`                                              |
| **Y-axis Limits**            | `ax.set_ylim([a, b])`  | Defines visible range for Y-axis.                                    | `ax.set_ylim([0, 2])`                                              |
| **Alpha + Line Width Combo** | `alpha`, `lw`          | Combine transparency and width for emphasis.                         | `ax.plot(x, y, lw=3, alpha=0.7)`                                   |

---

## 🧩 Example Code

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

fig = plt.figure(figsize=(6, 4), dpi=120)
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])

# Example with custom style
ax.plot(x, y,
        color='#1f77b4',       # Custom blue
        linewidth=2.5,          # Thick line
        linestyle='--',         # Dashed line
        alpha=0.8,              # Slightly transparent
        marker='o',             # Circle markers
        markersize=6,           # Medium marker size
        markerfacecolor='red',  # Red inside
        markeredgecolor='black',# Black border
        markeredgewidth=1)      # Border thickness

ax.set_xlim([0, 10])
ax.set_ylim([-1.5, 1.5])
ax.set_title('Customized Sine Wave')
ax.set_xlabel('X Axis')
ax.set_ylabel('Y Axis')

plt.show()
```
<img width="871" height="592" alt="image" src="https://github.com/user-attachments/assets/e6f503c8-a46c-43d2-b2a3-9bc6d760558c" />

---

## 📊 Specialized Plot Types

While `ax.plot()` creates line plots, Matplotlib supports many other plot types:

| **Plot Type** | **Function**   | **Purpose**                               |
| ------------- | -------------- | ----------------------------------------- |
| Bar Plot      | `ax.bar()`     | Compare categorical values                |
| Scatter Plot  | `ax.scatter()` | Show relationships between two variables  |
| Histogram     | `ax.hist()`    | Show distribution of numerical data       |
| Box Plot      | `ax.boxplot()` | Summarize data spread and detect outliers |

For more aesthetic statistical plots, libraries like **Seaborn** build on top of Matplotlib.

---

## 💡 Key Takeaways

* Use `color` or hex codes for full color control.
* Adjust `linewidth` and `alpha` to improve clarity and contrast.
* Use different `linestyle` and `marker` combinations to distinguish datasets.
* Control visible regions using `set_xlim()` and `set_ylim()`.
* For professional results, pair these customizations with proper labels, titles, and legends.

---

## 📚 Further Reading

* [Matplotlib Official Documentation](https://matplotlib.org/stable/gallery/index.html)
* [Matplotlib Color Reference](https://matplotlib.org/stable/gallery/color/named_colors.html)
* [Seaborn for Advanced Statistical Visualization](https://seaborn.pydata.org/)

