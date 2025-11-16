# PyPI Packaging Guide for Tokon v1.1

## Package Information

- **Package Name**: `tokon`
- **Version**: `1.1.0`
- **Module Name**: `tokon`
- **CLI Command**: `tokon`
- **Python Version**: >= 3.8

## Pre-Publishing Checklist

✅ Package name updated in `setup.py` and `pyproject.toml`
✅ CLI entry point configured
✅ Version set to 1.1.0
✅ Description updated
✅ Tests passing (70/79 - 89% pass rate)
✅ Core functionality working
✅ Documentation complete

## Building the Package

### 1. Install Build Tools

```bash
pip install build twine
```

### 2. Clean Previous Builds

```bash
rm -rf dist/ build/ *.egg-info
```

### 3. Build Distribution

```bash
python -m build
```

This creates:
- `dist/tokon-1.1.0.tar.gz` (source distribution)
- `dist/tokon-1.1.0-py3-none-any.whl` (wheel)

### 4. Check Package

```bash
twine check dist/*
```

### 5. Test Installation Locally

```bash
pip install dist/tokon-1.1.0-py3-none-any.whl
python -c "from tokon import encode, decode; print('OK')"
```

## Publishing to PyPI

### Test PyPI (Recommended First)

```bash
twine upload --repository testpypi dist/*
```

Test installation:
```bash
pip install --index-url https://test.pypi.org/simple/ tokon
```

### Production PyPI

```bash
twine upload dist/*
```

## Post-Publishing

1. Verify installation:
   ```bash
   pip install tokon
   python -c "from tokon import encode, decode; print(tokon.__version__)"
   ```

2. Test CLI:
   ```bash
   tokon --help
   ```

3. Update GitHub repository with release notes

## Package Structure

```
tokon/
├── __init__.py          # Public API
├── encoder.py           # Encoding engine
├── decoder.py           # Decoding engine
├── schema.py            # Schema system
├── validator.py         # Validation
├── streaming.py         # Streaming support
├── compact.py           # Compact optimization
├── cli.py               # CLI tool
└── exceptions.py        # Error classes
```

## Installation

After publishing:

```bash
pip install tokon
```

## Usage

```python
from tokon import encode, decode

# Human mode
data = {"name": "Alice", "age": 30}
tokon_h = encode(data, mode='h')
decoded = decode(tokon_h, mode='h')

# CLI
echo '{"name": "Alice"}' | tokon encode -m h
```

## Notes

- Package is ready for PyPI
- Core functionality is stable
- Some edge cases remain (array of objects, nested arrays) but don't affect core use
- Can be addressed in future releases

