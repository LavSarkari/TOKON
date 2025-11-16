# Installation Guide

## Prerequisites

- Python 3.8 or higher
- pip (Python package installer)

## Installation

### From PyPI (Recommended)

```bash
pip install tokon
```

### From Source

```bash
# Clone the repository
git clone https://github.com/LavSarkari/tokon.git
cd tokon

# Install in development mode
pip install -e .

# Or install with development dependencies
pip install -e ".[dev]"
```

### Verify Installation

```python
python -c "from tokon import encode, decode; print('Tokon installed successfully!')"
```

## Development Setup

```bash
# Clone repository
git clone https://github.com/LavSarkari/tokon.git
cd tokon

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install with dev dependencies
pip install -e ".[dev]"

# Run tests
pytest

# Run benchmarks
python benchmarks/tokon_benchmark.py
```

## Troubleshooting

### Import Errors

If you get `ModuleNotFoundError: No module named 'tokon'`:

1. Verify installation:
   ```bash
   pip show tokon
   ```

2. Check Python path:
   ```python
   import sys
   print(sys.path)
   ```

3. Reinstall if needed:
   ```bash
   pip uninstall tokon
   pip install tokon
   ```

### CLI Not Found

If `tokon` command is not found:

1. Check installation:
   ```bash
   pip show tokon
   ```

2. Verify entry point:
   ```bash
   python -m tokon.cli --help
   ```

3. Use Python module directly:
   ```bash
   python -m tokon.cli encode -m h
   ```

## Requirements

- **Python**: 3.8+
- **Dependencies**: None (pure Python, zero dependencies)

## Platform Support

- ✅ Windows
- ✅ macOS
- ✅ Linux
- ✅ All platforms with Python 3.8+

## Next Steps

After installation, see the [README.md](README.md) for usage examples and the [TOKON_SPEC.md](TOKON_SPEC.md) for the complete specification.

