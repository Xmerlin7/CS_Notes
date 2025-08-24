## 🐍 Python Core Notes (Advanced Level)

### 📌 Variables
- Python is dynamically typed; no need to declare types explicitly.
- Variables are references to objects in memory.
- Immutable types (e.g., `int`, `str`) create new objects upon change.
- Use descriptive names (e.g., `user_age` instead of `x`).

```python
x = 10      # integer
name = "Ali" # string
```

---

### 🧾 Receiving Input
- `input()` always returns a string; needs conversion if numeric.
- Common pattern:

```python
age = int(input("Enter your age: "))
```

---

### ⚡ Python Cheat Sheet (selected)
- `type(var)` → returns data type
- `dir(obj)` → list of available methods/attributes
- `help(obj)` → built-in docstring

---

### 🔄 Type Conversion
- Common conversions:
  - `int("123")`
  - `float("3.14")`
  - `str(10)`
  - `bool(0)` → `False`, all others → `True`
- Use `isinstance(x, type)` to check type before conversion when needed.

---

### 🧵 Strings
- Immutable sequences of Unicode characters.
- Indexed and sliced like lists.

```python
text = "Python"
print(text[0])    # P
print(text[-1])   # n
print(text[0:2])  # Py
```

---

### 🔧 Formatted Strings
- `f"{expression}"` is preferred.

```python
name = "Sara"
age = 25
print(f"{name} is {age} years old")
```

---

### 🔤 String Methods (Common)
- `str.upper()` / `str.lower()`
- `str.strip()`
- `str.find(sub)` → returns index or -1
- `str.replace(old, new)`
- `"in"` keyword for substring check

---

### ➕ Arithmetic Operations
| Operator | Description     |
|----------|-----------------|
| `+`      | Addition         |
| `-`      | Subtraction      |
| `*`      | Multiplication   |
| `/`      | Division (float) |
| `//`     | Floor division   |
| `%`      | Modulo           |
| `**`     | Power            |

---

### 🔢 Operator Precedence
| Level | Operators           |
|-------|----------------------|
| 1     | `()` (parentheses)   |
| 2     | `**` (exponentiation)|
| 3     | `+ - ~` (unary)      |
| 4     | `* / // %`           |
| 5     | `+ -` (binary)       |

Use parentheses for clarity.

---

### 🧮 Math Functions
- From `math` module:
```python
import math
math.ceil(1.2)
math.floor(1.2)
math.sqrt(9)
math.pow(2, 3)
```

---

### 🔀 If Statements
```python
if condition:
    ...
elif condition:
    ...
else:
    ...
```
- Truthy values: non-zero numbers, non-empty strings/containers

---

### 🔗 Logical Operators
| Operator | Meaning        |
|----------|----------------|
| `and`    | Both True       |
| `or`     | At least one    |
| `not`    | Negation        |

---

### ⚖️ Comparison Operators
- `==`, `!=`, `>`, `<`, `>=`, `<=`
- Chainable: `0 < x < 10`
- `is` compares identity; `==` compares values

---

### 🔁 While Loops
```python
while condition:
    ...
```
- `break` → exits loop
- `continue` → skips iteration
- Beware infinite loops (ensure exit condition)

---

### 🔁 For Loops
```python
for item in iterable:
    ...
```
- Works with `str`, `list`, `tuple`, `range()` etc.

```python
for i in range(5):
    print(i)
```

---

### 🧊 Nested Loops
- Loops inside loops:
```python
for x in range(3):
    for y in range(2):
        print(x, y)
```
- Inner loop runs completely for each outer iteration.

---

- Useful methods: `append()`, `insert()`, `remove()`, `pop()`, `index()`
## 🔒 Tuples vs Lists vs Dictionaries

### ✅ Tuples
- Immutable, ordered sequences.
- Syntax: `t = (1, 2, 3)`
- Cannot add/remove/change elements.
- Faster than lists due to immutability.
- Used as keys in dictionaries (if all elements are immutable).
- Supports unpacking:
```python
a, b = (1, 2)
```

### ✅ Lists
```python
nums = [1, 2, 3]
nums.append(4)
nums[0] = 10
```
- Mutable, ordered.
- Syntax: `l = [1, 2, 3]`
- Can modify contents.
- Heavier memory-wise and slower than tuples.
- Common for collections of similar items.
- Slicing, concatenation, iteration
- Useful methods: `.append()`, `.insert()`, `.remove()`, `.pop()`
## 🧱 2D Lists
```python
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
print(matrix[1][2])  # → 6
```
- Often accessed via nested loops.
### ✅ Dictionaries
- Unordered (in older versions), mutable mappings.
- Syntax: `d = {"key": "value"}`
- Key-value pairs.
- Keys must be hashable (strings, numbers, tuples).
- Values can be any type.
- Useful methods: `.get()`, `.items()`, `.keys()`, `.values()`

### 🚨 Comparison Summary
| Feature       | Tuple        | List         | Dictionary             |
|---------------|--------------|--------------|------------------------|
| Ordered       | ✅           | ✅           | ❌ (✅ from 3.7+)       |
| Mutable       | ❌           | ✅           | ✅                     |
| Indexable     | ✅           | ✅           | ❌ (by keys instead)   |
| Hashable      | ✅ (if pure) | ❌           | ❌                     |
| Use Case      | Fixed data   | Dynamic data | Key-value mapping      |

---

> ✅ Use tuples when your data should not change.
> ✅ Use lists when you need to modify the collection.
> ✅ Use dictionaries when working with named data / mappings.
