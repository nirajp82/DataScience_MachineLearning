# Matplotlib: Figures, Axes, Axis, and Plots

---

## Quick mental model

* **Figure** = the entire *canvas* (a window, a page, or an image). Holds one or more Axes.
* **Axes** (class name is `Axes`) = the *plotting area* (a single subplot region). Contains Axis objects, artists, labels, title, legend, etc.
* **Axis** = one coordinate axis (e.g., x-axis or y-axis) inside an Axes. Handles ticks, ticklabels, scale, locator/formatters.
* **Plot** = the actual data drawing (lines, bars, scatter points). These are *artists* (e.g., `Line2D`) drawn inside an Axes.

**Hierarchy:**

```
Figure → Axes → Axis (x/y) + Artists (Line2D, Patch, Text, Image, Colorbar...)
```

> ✅ A critical rule: **`plot()` is a method of `Axes`, not of `Figure`. So you should always do:**
>
> ```python
> ax.plot(x, y)  # correct when using object-oriented Matplotlib
> ```
>
> Using `plt.plot(...)` uses pyplot's state-machine which implicitly creates/uses the current Axes — fine for quick scripts, but prefer `ax.plot()` in larger code.

---

# 1. Figure (the canvas)

**Creation:**

```python
fig = plt.figure(figsize=(6, 4), dpi=100)
```

**Important points:**

* `figsize=(width, height)` is in **inches**.
* `dpi` is **dots per inch** (pixels per inch). Total pixel dimensions = `figsize * dpi`.
* Default values come from `matplotlib.rcParams` (e.g., `rcParams['figure.figsize']`, `rcParams['figure.dpi']`).
* You can change size after creation: `fig.set_size_inches(w, h)`.
* `Figure` contains methods like `savefig`, `add_axes`, `add_subplot`, `subplots_adjust`, and attributes like `fig.canvas`.

**Saving:**

```python
fig.savefig('file.png', dpi=300, bbox_inches='tight', transparent=False)
```

* `savefig(..., dpi=...)` overrides the figure's `dpi` for the saved file.
* `bbox_inches='tight'` attempts to crop excess whitespace; pair with `pad_inches` if required.
* For *publication-quality* use `dpi=300` (PNG) or export to vector formats (`pdf`, `svg`) for lossless scaling.

**Vector vs Raster:**

* Vector formats (`pdf`, `svg`, `eps`) scale without losing quality and are preferred for line-art and text.
* Raster formats (`png`, `jpg`) depend on DPI; increase `dpi` for higher resolution.

---

# 2. Axes (the plot area)

**Create axes manually:**

```python
ax = fig.add_axes([left, bottom, width, height])
```

* Coordinates are **fractions of the figure** (0–1) by default. Example: `[0.1, 0.1, 0.8, 0.8]`.
* `add_axes([0,0,1,1])` makes the axes fill the entire figure (no margins) — useful for image plots or custom renderings.

**Create axes via convenience helpers:**

```python
fig, ax = plt.subplots(nrows=1, ncols=1, figsize=(6,4), dpi=100)
```

* `plt.subplots()` is the most common pattern; it creates a Figure and an Axes (or an array of Axes) for you.
* `fig.add_subplot(111)` creates a single Axes via a subplot index; it’s equivalent to `plt.subplot(111)`.

**Axes properties & methods (common):**

* `ax.plot(x, y)`, `ax.bar(...)`, `ax.scatter(...)`, `ax.imshow(...)` — draw data (artists).
* `ax.set_title('Title')`, `ax.set_xlabel('x')`, `ax.set_ylabel('y')` — labeling.
* `ax.set_xlim()`, `ax.set_ylim()` — control axis limits.
* `ax.legend()` — place legend (use `loc` or `bbox_to_anchor`).
* `ax.twinx()`, `ax.twiny()` — create a shared x or y axis.
* `ax.inset_axes()` or `mpl_toolkits.axes_grid1.inset_locator` — for inset axes (requires helpers).
* `ax.get_position()` / `ax.set_position()` — read/set the axes bounding box in figure coordinates.

**Multiple Axes:**

* `plt.subplots(nrows, ncols)` returns `axes` as a 2D array when `nrows>1` or `ncols>1` — use `axes.ravel()` or `axes.flatten()` to iterate.
* `GridSpec` provides fine-grained control over subplot grid sizing and spanning.

---

# 3. Axis (the coordinate axis)

* Each `Axes` has `ax.xaxis` and `ax.yaxis` (instances of `matplotlib.axis.Axis`).
* Axis manages ticks, tick labels, locators, and formatters. Examples:

  * `ax.xaxis.set_major_locator(...)`
  * `ax.xaxis.set_major_formatter(...)`
  * `ax.tick_params(axis='x', rotation=45)`

**Common methods:**

* `ax.set_xticks([...])`, `ax.set_xticklabels([...])`
* `ax.xaxis.set_major_locator(mticker.MaxNLocator(n))`
* `ax.yaxis.set_major_formatter(mticker.FuncFormatter(func))`

---

# 4. Artists & Plots

* Everything drawn in Matplotlib is an **Artist** (the Artist hierarchy). Examples: `Line2D` (from `ax.plot()`), `Rectangle` (bars), `Text`, `Image`.
* `ax.plot()` returns a list of `Line2D` objects. You can keep references for further control:

  ```python
  lines = ax.plot(x, y)
  line = lines[0]
  line.set_linewidth(2)
  line.set_color('C1')
  ```

---

# 5. State-machine (pyplot) vs Object-oriented style

* `import matplotlib.pyplot as plt` provides a *state-machine* interface. `plt.plot(x,y)` implicitly finds or creates the current Axes.
* **Prefer the object-oriented style** in real code: create `fig` and `ax` and call `ax.plot()` (clearer scope, easier testing, less implicit behavior).
* **Important**: `plot()` is a method of **Axes**, not Figure. Using `plt.plot()` is okay for quick sketches but can create bugs in complex scripts.

---

# 6. Layout management: spacing and clipping

* **Default margins** from `plt.subplots()` are usually fine; for manual control use:

  * `plt.tight_layout()` — automatically adjusts subplots to fit into the figure area without overlapping labels. Works for most cases.
  * `fig.set_constrained_layout(True)` or `plt.subplots(constrained_layout=True)` — newer, more robust layout engine (works well with complex nested grids and colorbars).
  * `fig.subplots_adjust(left=..., bottom=..., right=..., top=..., wspace=..., hspace=...)` — manual control.

**Clipping warnings:**

* Text and tick labels can be clipped (especially with `add_axes([0,0,1,1])` or small figsize). Use `tight_layout()` or `bbox_inches='tight'` when saving.

---

# 7. DPI, figsize, and pixel math

* Pixel Width = `figsize[0] * dpi`
* Pixel Height = `figsize[1] * dpi`

**Examples:**

* `figsize=(3,2), dpi=100` → 300×200 px (small, low-res)
* `figsize=(6,4), dpi=300` → 1800×1200 px (high-res, publication quality)

**When to change what:**

* Increase **`dpi`** to increase *resolution* without changing physical size.
* Increase **`figsize`** to increase *physical size* (layout room for labels and multiple subplots).
* You can override DPI on save: `fig.savefig('out.png', dpi=300)`.

**Fonts and DPI:**

* Text sizes given in points will scale with DPI at save time. If you rely on consistent physical sizes in print, test with the final DPI.
* `rcParams['font.size']` and `rcParams['figure.dpi']` allow global defaults.

---

# 8. Saving: practical options & gotchas

```python
fig.savefig('plot.png', dpi=300, bbox_inches='tight', pad_inches=0.02, transparent=False)
```

* `dpi` - final resolution for raster output.
* `bbox_inches='tight'` - trim white space (may crop legend if it’s outside the axes unless you use `bbox_extra_artists`).
* `transparent=True` - saves image with alpha background (useful for overlays on web/UI).
* `format='pdf'` or filename ending in `.pdf` → vector output.

**To ensure crisp text:** prefer vector (`pdf`, `svg`) when possible.

---

# 9. Advanced/Useful features (short list)

* **GridSpec**: flexible subplot layout control.
* **Inset axes**: `ax.inset_axes(...)` or `mpl_toolkits.axes_grid1.inset_locator` for zoomed insets.
* **Colorbars**: use `fig.colorbar(im, ax=ax)` or `make_axes_locatable` for an independent colorbar axis.
* **Twin axes**: `ax.twinx()` or `ax.secondary_xaxis()` for different scales.
* **Transforms**: `ax.transData`, `fig.transFigure` — for advanced positioning.
* **zorder** controls draw order (higher `zorder` drawn on top).
* **Rasterization**: set `rasterized=True` on complex artists when saving vector files to speed saves and reduce file size.

---

# 10. Common pitfalls and tips (explicit!)

* **`plot()` belongs to `Axes`**: always prefer `ax.plot()` when writing functions or libraries.
* Using `add_axes([0,0,1,1])` will remove margins — titles or ticklabels may be clipped.
* `plt.show()` behavior depends on backend and interactive mode:

  * In scripts, use `plt.show()` to pop up windows (blocking by default).
  * Interactive shells (Jupyter) may auto-display; `plt.ion()` enables interactive mode.
* When subplots are returned as arrays, use `axes.flat` or `axes.ravel()` to iterate.
* Legends outside the axes: use `bbox_to_anchor` or `loc='upper left', bbox_to_anchor=(1,1)` and `fig.tight_layout()` / `bbox_inches='tight'` on save.
* To change a figure’s DPI post-creation: `fig.set_dpi(new_dpi)` or set when saving.
* If elements overlap, try `plt.tight_layout()` first, then `constrained_layout` if available.

---

# 11. Example recipes (copy-paste)

**A — Full-figure axes (your example)**

```python
fig = plt.figure(figsize=(3, 2), dpi=100)
ax = fig.add_axes([0, 0, 1, 1])
ax.plot(x, y)
# Save at higher DPI if needed:
fig.savefig('full_figure.png', dpi=300)
```

**B — High-resolution plot for publication**

```python
fig, ax = plt.subplots(figsize=(6, 4), dpi=300)
ax.plot(x, y)
ax.set_title('High-res plot')
fig.savefig('fig_pub.png', dpi=300)
```

**C — Grid of subplots with shared axes**

```python
fig, axes = plt.subplots(2, 2, figsize=(8, 6), sharex=True, sharey=False)
for ax in axes.ravel():
    ax.plot(x, np.sin(x + np.random.rand()))
fig.tight_layout()
```

**D — Legend outside with tight saving**

```python
fig, ax = plt.subplots(figsize=(6,4))
ax.plot(x, y, label='line')
ax.legend(loc='upper left', bbox_to_anchor=(1.02, 1.0))
fig.savefig('legend_outside.png', bbox_inches='tight', dpi=300)
```

---

# 12. Cheat sheet (most used APIs)

* Create figure: `fig = plt.figure(figsize=(w,h), dpi=xx)`
* Create fig+ax: `fig, ax = plt.subplots(figsize=(w,h))`
* Add axes: `ax = fig.add_axes([l,b,w,h])`
* Plot: `ax.plot(x,y)`  ⚠️ (not `fig.plot`)
* Label: `ax.set_xlabel(...)`, `ax.set_ylabel(...)`, `ax.set_title(...)`
* Limits: `ax.set_xlim(a,b)`, `ax.set_ylim(a,b)`
* Legend: `ax.legend()` or `ax.legend(loc='best')`
* Save: `fig.savefig('name.png', dpi=300, bbox_inches='tight')`
* Layout: `fig.tight_layout()` / `fig.set_constrained_layout(True)`
* Subplots grid: `fig, axes = plt.subplots(nrows, ncols)`

---

# 13. Final tips & best practices

* Use **object-oriented API** (`fig, ax = plt.subplots()` and `ax.*`) for reproducible, modular code.
* Prefer **vector output** for plots containing text/lines to prevent rasterization artifacts in publications.
* Use `dpi` and `figsize` together to control the final pixel size for raster exports.
* Start with `plt.subplots()` and only use `add_axes()` when you need absolute control.
* Keep `plot()` calls scoped to `ax` to avoid accidental plotting onto the wrong axes.


Happy plotting! 🎨📊
