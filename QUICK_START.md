# Quick Start Guide

Get started with Tokon in 5 minutes!

## Installation

```bash
pip install tokon
```

## Basic Usage

### 1. Simple Encoding/Decoding

```python
from tokon import encode, decode

# Your data
data = {
    "name": "Alice",
    "age": 30,
    "active": True
}

# Encode to human-readable format
tokon_h = encode(data, mode='h')
print(tokon_h)
# Output:
# name Alice
# age 30
# active true

# Decode back
decoded = decode(tokon_h, mode='h')
print(decoded)
# Output: {'name': 'Alice', 'age': 30, 'active': True}
```

### 2. Compact Mode

```python
from tokon import encode, decode

data = {"name": "Alice", "age": 30}
tokon_c = encode(data, mode='c')
print(tokon_c)
# Output: name:Alice age:30

decoded = decode(tokon_c, mode='c')
```

### 3. With Schema (Recommended for Production)

```python
from tokon import encode, decode, load_schema

# Load schema
schema = load_schema('user.tks')

# Encode with schema (compact mode)
data = {"name": "Alice", "age": 30, "active": True}
tokon_c = encode(data, mode='c', schema=schema)
print(tokon_c)
# Output: n:Alice a:30 x:1

# Decode with schema
decoded = decode(tokon_c, mode='c', schema=schema)
```

## Command Line

```bash
# Encode JSON to Tokon
echo '{"name": "Alice", "age": 30}' | tokon encode -m h

# Decode Tokon to JSON
echo 'name Alice\nage 30' | tokon decode
```

## Next Steps

- Read [USAGE.md](USAGE.md) for detailed examples
- See [INSTALLATION.md](INSTALLATION.md) for setup
- Check [TOKON_SPEC.md](TOKON_SPEC.md) for specification

## Common Patterns

### Configuration File

```python
config = {
    "app": {
        "name": "MyApp",
        "version": "1.0.0",
        "debug": True
    }
}

tokon = encode(config, mode='h')
# Save to config.tokon
```

### API Response

```python
response = {
    "users": [
        {"id": 1, "name": "Alice"},
        {"id": 2, "name": "Bob"}
    ]
}

# Use compact mode for efficiency
tokon_c = encode(response, mode='c', schema=user_schema)
```

That's it! You're ready to use Tokon. 🚀

