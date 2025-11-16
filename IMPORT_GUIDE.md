# Import Guide - Fix Your Import Errors

## The Problem

You're getting this error:
```
ImportError: cannot import name 'encode' from partially initialized module 'toon'
```

**Root Cause:** You have a local file `toon.py` in your home directory that conflicts with the installed package.

## Quick Fix

### Step 1: Remove the Conflicting File

```bash
# Rename your local toon.py file
mv ~/toon.py ~/my_toon_script.py

# Or delete it if you don't need it
rm ~/toon.py
```

### Step 2: Use Correct Import

```python
# After: pip install tokon
# Import using the MODULE name 'toon', not the package name 'tokon'

from toon import encode, decode

# Now it works!
data = {
    "items": [
        {"sku": "A1", "qty": 2, "price": 9.99},
        {"sku": "B2", "qty": 1, "price": 14.5}
    ]
}

print(encode(data))
```

## Understanding Package vs Module Name

- **Package name (PyPI):** `tokon` → `pip install tokon`
- **Module name (Python):** `toon` → `from toon import encode`

They are **different**! The package name doesn't match the module name.

## Complete Working Example

```bash
# 1. Install
pip install tokon

# 2. Make sure no toon.py file exists in your directory
ls ~/toon.py  # If it exists, rename it!

# 3. Create a new script (NOT named toon.py!)
cat > test_tokon.py << 'EOF'
from toon import encode, decode

data = {"name": "Alice", "age": 30}
result = encode(data)
print(result)

decoded = decode(result)
print(decoded)
EOF

# 4. Run it
python test_tokon.py
```

## Why This Happens

Python searches for modules in this order:
1. Current directory first
2. Then installed packages

If you have `toon.py` in your current directory, Python finds that first and tries to import from it, causing the conflict.

## Verification

To verify the package is installed correctly:

```python
import toon
print(toon.__version__)  # Should print: 0.1.0
print(toon.__all__)      # Should show: ['encode', 'decode', ...]
```

If this works, the package is fine - you just need to remove the conflicting file!

