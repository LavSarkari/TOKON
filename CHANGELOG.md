# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-01-16

### Added
- Initial release of Tokon v1.1
- Dual-mode architecture (Tokon-H and Tokon-C)
- Schema system with .tks file support
- Type validation and schema validation
- Streaming support (Tokon-S)
- Command-line interface (CLI)
- Comprehensive test suite
- Complete documentation and specification

### Features
- **Tokon-H (Human Mode)**: Clean, readable, indentation-based format
- **Tokon-C (Compact Mode)**: Ultra-compact, schema-optimized format
- **Schema System**: Symbol mapping, type definitions, multilingual support
- **Validation**: Type checking and schema validation
- **Streaming**: Incremental parsing for large datasets
- **CLI Tool**: Command-line encoding/decoding
- **Auto-detection**: Automatic mode detection

### Performance
- 53% token reduction vs JSON (H-mode)
- 78% token reduction vs JSON (C-mode)
- Fast encoding/decoding performance

### Documentation
- Complete specification (TOKON_SPEC.md)
- Installation guide (INSTALLATION.md)
- Usage guide (USAGE.md)
- API reference
- Examples and benchmarks
