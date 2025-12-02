---
id: 5a1d3848-e608-40cc-83a9-1d96452dbf6a
aliases:
  - exceptions-type-hints-json
tags: []
---

# exceptions-type-hints-json

## Week 2: Exceptions, Type Hints & JSON

## 1. Type Hints (Writing modern Python)
Python is "dynamically typed" (you don't *have* to declare types), but in professional code, we use **Type Hints**. They help editors (VS Code) catch bugs before you run the code.

```python
# Old Python
def add(a, b):
    return a + b

# Modern Python (Professional)
# We specify that inputs must be floats, and it returns a float.
def add(a: float, b: float) -> float:
    return a + b
```

## 2. Docstrings (Documentation)
Every function should have a "Docstring" explaining what it does. This allows tools to auto-generate documentation later.

```Python
def divide(a: float, b: float) -> float:
    """
    Divides a by b.
    
    Args:
        a (float): The numerator
        b (float): The denominator
        
    Returns:
        float: The result of the division
    """
    return a / b
```
## 3. Exception Handling (try / except)
Bad code crashes when an error happens. Good code "catches" the error and handles it.

```Python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("You cannot divide by zero!")
    result = 0
except ValueError:
    print("Please enter a valid number.")
```

Common Exceptions:
- `ZeroDivisionError`: Math error.
- `ValueError`: Wrong type of value (e.g., converting "abc" to int).
- `FileNotFoundError`: Trying to open a missing file.

## 4. JSON (Saving Data)
Variables die when the script ends. To keep data (History), we write it to a file. JSON is the standard format for this.

```Python
import json
from pathlib import Path

# Data to save
history = [
    {"op": "add", "a": 5, "b": 3, "result": 8},
    {"op": "div", "a": 10, "b": 2, "result": 5}
]

file_path = Path("history.json")

# WRITING (Saving)
with open(file_path, "w") as f:
    json.dump(history, f, indent=4) # indent makes it readable

# READING (Loading)
if file_path.exists():
    with open(file_path, "r") as f:
        data = json.load(f)
        print(data)
```

## 5. Project Structure
For Week 2, we will create a new folder next to `folder_organizer`:

```Text
python-job-ready/          (Root Repo)
├── folder_organizer/      (Week 1 Project)
└── cli_calculator/        (Week 2 Project)
    ├── main.py            # Entry point
    ├── calculator.py      # Math logic
    ├── history.py         # JSON logic
    └── tests/
```