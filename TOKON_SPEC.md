# Tokon v1.1 Specification

**Token-Optimized, AI-Native Dual-Mode Serialization Format**

> **Note:** Tokon is inspired by the [TOON format](https://github.com/toon-format/toon) but is a completely original implementation with dual-mode architecture and schema-driven optimization.

## Executive Summary

Tokon v1.1 is a dual-mode, schema-driven serialization format designed specifically for AI-native workflows. It introduces two distinct yet interconnected representations:

* **Tokon‑H (Human Mode):** A clean, indentation‑based, highly readable structure designed for clarity, collaboration, fast debugging, education, and expressive modeling.
* **Tokon‑C (Compact Mode):** An ultra‑compact, symbol‑mapped, token‑efficient structure designed to minimize LLM tokenization cost and maximize computational efficiency.

Tokon provides deterministic grammar, a multilingual schema system, strong type validation, a streaming framework, predictable formatting rules, and significant performance advantages over JSON, YAML, and minimalistic formats.

---

## 2. Motivation

Modern AI systems rely on structured data for prompt engineering, tool output, agent memory, and inter‑component communication. Existing formats cause three major issues:

1. **Verbosity:** JSON and YAML repeat long keys and deep structures.
2. **Token Waste:** LLMs tokenize characters, not meaning. Unnecessary punctuation increases cost.
3. **Human vs Machine Conflict:** Human‑readable formats differ from compact forms.

Tokon resolves all three simultaneously via its dual‑mode architecture.

---

## 3. Tokon Design Philosophy

1. **AI‑First, Human‑Compatible**: Build for LLM interpretation first, without sacrificing clarity.
2. **Deterministic**: No ambiguous parsing, no loose grammar.
3. **Two‑Layer Format**: Human Mode for clarity, Compact Mode for efficiency.
4. **Schema‑Driven Intelligence**: Symbols, languages, defaults, validation.
5. **Predictable Token Flow**: Symbols selected for single‑token efficiency.
6. **Extensible Architecture**: Tokon-S streaming, future binary mode, stable token IDs.

---

## 4. Formal Grammar (EBNF Overview)

### 4.1 Tokon‑H Grammar

```
Document      = Block ;
Block         = Key Newline Indent Content ;
Content       = (Key Value Newline)* (Block)* ;
Key           = Identifier ;
Value         = Primitive | Identifier ;
Indent        = "  " ; // 2 spaces
Primitive     = String | Number | Boolean | Null ;
Identifier    = Letter { Letter | Digit | "_" } ;
```

### 4.2 Tokon‑C Grammar

```
Document        = SymbolBlock ;
SymbolBlock     = Symbol "[" Items "]" ;
Items           = (Pair | SymbolBlock | Primitive)* ;
Pair            = Symbol ":" Primitive ;
Symbol          = Letter { Letter | Digit } ; // 1-2 chars
Primitive       = String | Number | Boolean ;
```

---

## 5. Tokon‑H (Human Mode)

### 5.1 Structure Rules

1. Two spaces define hierarchy.
2. `key value` pairs.
3. Arrays: repeated keys or indented values.
4. No punctuation.
5. Whitespace is structural.

### 5.2 Examples

```
user
  name Alice
  age 30
  active true
  tags
    python
    ai
    serialization
```

```
orders
  order
    id 12345
    total 99.99
  order
    id 12346
    total 149.50
```

---

## 6. Tokon‑C (Compact Mode)

### 6.1 Structure Rules

1. Blocks use `[ ]`.
2. Symbols replace keys (from schema).
3. `symbol:value` for assignments.
4. Arrays inline inside blocks.

### 6.2 Examples

```
u[n:Alice a:30 x:1 t[py ai ser]]
```

```
o[o[i:12345 i[i[s:A1 q:2 p:9.99]]] o[i:12346 i[i[s:B2 q:1 p:14.5]]]]
```

---

## 7. Schema System (.tks)

### 7.1 Schema Capabilities

* Symbol mapping
* Multilingual keys
* Type definitions
* Validation rules
* Default values

### 7.2 Example Schema

```
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

  languages {
    en: { name: "name" age: "age" }
    es: { name: "nombre" age: "edad" }
  }

  defaults {
    active: true
  }
}
```

---

## 8. Type System

Supported types:

* str
* int
* float
* bool
* null
* list[T]
* object
* date
* enum

---

## 9. Streaming (Tokon‑S)

Supports incremental chunk parsing.

Example chunks:

```
user
  name Alice
```

```
  age 30
  active true
```

---

## 10. Token Efficiency Benchmarks

### Test Payload: ~180 JSON tokens

| Format  | Tokens | Reduction |
| ------- | ------ | --------- |
| JSON    | 180    | —         |
| Tokon‑H | 85     | 53%       |
| Tokon‑C | 40     | 78%       |

### Methodology

1. Prompt encoded via GPT tokenizer.
2. Symbol set chosen for single-token behavior.
3. Repeated keys fully collapsed.

---

## 11. Comparison With Other Formats

### JSON

* ✔ universal
* ❌ verbose
* ❌ token‑heavy
* ❌ extra punctuation

### YAML

* ✔ human-friendly
* ❌ ambiguous grammar
* ❌ whitespace pitfalls

### TOML

* ✔ configs
* ❌ limited structure

### XML

* ❌ extreme verbosity

### Toon

* ✔ minimal
* ❌ lacks schema mapping
* ❌ not AI‑optimized
* ❌ not dual‑mode

### Tokon

* ✔ dual-mode
* ✔ schema-driven
* ✔ AI-native
* ✔ highest token reduction
* ✔ multilingual

---

## 12. Error Handling

```
TokonSyntaxError: Unexpected token at line 4
Expected: key value pair
```

Types:

* TokonSyntaxError
* TokonSchemaError
* TokonTypeError
* TokonDecodeError
* TokonEncodeError

---

## 13. Limitations

* Requires schema for compact mode
* Indentation errors possible in human mode
* Current version lacks binary mode

---

## 14. Security Considerations

* No code execution
* Deterministic parsing prevents injection
* Schemas restrict malicious fields

---

## 15. Future Roadmap (Tokon v2.0)

* Binary mode (Tokon‑B)
* Stable Token IDs
* AI‑adaptive schemas
* Compressed streaming frames
* Structural fingerprints for caching

---

## 16. Reference Implementation (Python)

API:

```
encode(data, mode='h'|'c')
decode(text, mode='auto')
load_schema(path)
```

Core modules:

* tokon_schema
* tokon_encoder
* tokon_decoder
* tokon_validator
* tokon_streaming
* tokon_compact

---

## 17. License

MIT License
