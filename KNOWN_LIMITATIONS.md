# Known Limitations

Tokon v1.1 has a few edge case limitations that don't affect core functionality:

## Current Limitations

1. **Array of Objects in H-mode**: Arrays of objects may not parse correctly in some edge cases. Workaround: Use compact mode with schemas for arrays of objects.

2. **Nested Arrays**: Deeply nested arrays may flatten in some cases. Workaround: Use compact mode for complex nested structures.

3. **Empty Structures**: Empty arrays and empty objects may be confused in edge cases. Workaround: Use explicit type hints in schemas.

4. **Deep Nesting**: Very deeply nested structures (4+ levels) may have parsing issues in H-mode. Workaround: Use compact mode for deeply nested data.

## Core Functionality

✅ All core features work correctly:
- Simple objects and arrays
- Nested objects (up to 3 levels)
- Primitive types
- Schema system
- Compact mode
- Human mode (for most use cases)
- Round-trip encoding/decoding

## Recommendations

- **Use Tokon-H** for: Simple to moderately nested structures, human-readable files, configuration
- **Use Tokon-C** for: Complex structures, arrays of objects, deeply nested data, LLM workflows

These limitations will be addressed in future releases.

