# Usage Guide

## Basic Usage

### Encoding Python Objects

```python
from tokon import encode

# Simple object
data = {"name": "Alice", "age": 30}
tokon_h = encode(data, mode='h')
print(tokon_h)
# name Alice
# age 30

# Compact mode
tokon_c = encode(data, mode='c')
print(tokon_c)
# name:Alice age:30
```

### Decoding Tokon Strings

```python
from tokon import decode

# Human mode
tokon_h = "name Alice\nage 30"
data = decode(tokon_h, mode='h')
print(data)
# {'name': 'Alice', 'age': 30}

# Auto-detect mode
data = decode(tokon_h, mode='auto')
```

## Working with Schemas

### Creating a Schema

Create a file `user.tks`:

```tks
schema user {
  symbols {
    name → n
    age → a
    active → x
    tags → t
  }
  
  types {
    name: str
    age: int
    active: bool
    tags: list[str]
  }
}
```

### Using Schemas

```python
from tokon import load_schema, encode, decode

# Load schema
schema = load_schema('user.tks')

# Encode with schema (compact mode)
data = {"name": "Alice", "age": 30, "active": True}
tokon_c = encode(data, mode='c', schema=schema)
print(tokon_c)
# n:Alice a:30 x:1

# Decode with schema
decoded = decode(tokon_c, mode='c', schema=schema)
```

## Advanced Examples

### Nested Objects

```python
data = {
    "user": {
        "name": "Alice",
        "settings": {
            "theme": "dark",
            "notifications": True
        }
    }
}

tokon_h = encode(data, mode='h')
# user
#   name Alice
#   settings
#     theme dark
#     notifications true
```

### Arrays

```python
# Array of primitives
data = {"tags": ["python", "ai", "serialization"]}
tokon_h = encode(data, mode='h')
# tags
#   python
#   ai
#   serialization

# Array of objects
data = {
    "orders": [
        {"id": 12345, "total": 99.99},
        {"id": 12346, "total": 149.50}
    ]
}
tokon_h = encode(data, mode='h')
# orders
#   order
#     id 12345
#     total 99.99
#   order
#     id 12346
#     total 149.50
```

### Validation

```python
from tokon import TokonValidator, load_schema

schema = load_schema('user.tks')
validator = TokonValidator(schema)

data = {"name": "Alice", "age": 30}
is_valid = validator.validate(data)  # True

# Strict validation (raises on error)
validator.validate_strict(data)
```

### Streaming

```python
from tokon import TokonStream

stream = TokonStream(mode='h')

# Feed chunks incrementally
stream.feed("user\n")
stream.feed("  name Alice\n")
stream.feed("  age 30\n")

# Get result
result = stream.finish()
print(result)
# {'user': {'name': 'Alice', 'age': 30}}
```

## Command Line Usage

### Encoding

```bash
# From JSON
echo '{"name": "Alice", "age": 30}' | tokon encode -m h

# From file
tokon encode -m h -i data.json -o output.tokon

# With schema
tokon encode -m c -s user.tks -i data.json
```

### Decoding

```bash
# To JSON
echo 'name Alice\nage 30' | tokon decode

# Pretty print
tokon decode -p -i data.tokon

# With schema
tokon decode -m c -s user.tks -i data.tokon
```

## Best Practices

1. **Use Tokon-H for human-readable files** - easier to debug and edit
2. **Use Tokon-C for LLM workflows** - maximum token efficiency
3. **Create schemas for repeated structures** - consistent symbols across project
4. **Validate data with schemas** - catch errors early
5. **Use streaming for large datasets** - process incrementally

## Common Patterns

### Configuration Files

```python
# config.tokon (H-mode)
app
  name MyApp
  version 1.0.0
  settings
    debug true
    port 8080
```

### API Responses

```python
# Compact mode for API responses
response = {
    "users": [
        {"id": 1, "name": "Alice"},
        {"id": 2, "name": "Bob"}
    ]
}
tokon_c = encode(response, mode='c', schema=user_schema)
# Minimal token usage for LLM processing
```

### Data Exchange

```python
# Encode for transmission
data = {"message": "Hello", "timestamp": 1234567890}
tokon = encode(data, mode='h')

# Decode on receiving end
received_data = decode(tokon, mode='auto')
```

## Error Handling

```python
from tokon import decode, TokonDecodeError

try:
    data = decode(invalid_tokon, mode='h')
except TokonDecodeError as e:
    print(f"Decode error: {e}")
```

## Performance Tips

1. **Use compact mode** for production LLM workflows
2. **Cache schemas** - load once, reuse many times
3. **Stream large files** - don't load everything into memory
4. **Validate early** - catch schema errors before encoding

## See Also

- [README.md](README.md) - Overview and quick start
- [TOKON_SPEC.md](TOKON_SPEC.md) - Complete specification
- [INSTALLATION.md](INSTALLATION.md) - Installation guide

