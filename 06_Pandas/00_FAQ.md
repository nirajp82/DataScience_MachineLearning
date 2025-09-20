### ❓ Why do we use `&` and `|` in Pandas instead of Python’s `and` / `or`?

**Answer:**
Python’s built-in `and` / `or` operators work only with **single boolean values**, not with arrays or Series.
For example:

```python
True and False   # ✅ Works → False

[True, False, True] and [False, True, True]  
# ❌ Error: cannot "and" lists element-wise
```

But in Pandas, a condition like:

```python
df['Age'] > 25
```

returns a **Series of booleans**, not one `True`/`False`:

```
0    False
1     True
2     True
Name: Age, dtype: bool
```

To combine these **element-wise**, Pandas (built on NumPy) reuses **bitwise operators**:

* `&` → element-wise AND
* `|` → element-wise OR
* `~` → element-wise NOT

Example:

```python
(df['Age'] > 25) & (df['City'] == "Chicago")
```

Output:

```
0    False
1    False
2     True
dtype: bool
```

⚠️ Always use **parentheses** around each condition because comparison operators (`>`, `==`, etc.) have higher precedence than `&` and `|`.

✅ **Summary:**

* Use `&` instead of `and` → element-wise AND
* Use `|` instead of `or` → element-wise OR
* Use `~` instead of `not` → element-wise NOT

---
