# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-06-20

### Added
- `generateMarkdown()` — convert JSON Schema objects to markdown documentation
- `resolveRef()` — resolve local `$ref` pointers (`#/definitions/...`, `#/$defs/...`)
- CLI tool `jsonschema-tomd` with `-o`, `-t`, `--max-depth` options
- Property tables with name, type, required, default, description columns
- Constraint rendering (min/max, minLength/maxLength, pattern, uniqueItems, etc.)
- Composition keyword support (`allOf`, `anyOf`, `oneOf`)
- Array item documentation (single schema + tuple validation)
- Nested property rendering with configurable depth limit
- `$defs` / `definitions` section rendering
- Example output in fenced JSON code blocks
- Deprecated field marking (⚠️)
- Additional properties documentation (allowed/forbidden)
- JSON pointer escape handling (`~0`, `~1`)
- 57 tests covering all public API surface

### Changed
- Nothing (initial release)

### Deprecated
- Nothing

### Removed
- Nothing

### Fixed
- Nothing

### Security
- Zero dependencies
- File reads use `path.resolve()` to prevent traversal
- No `eval()` or dynamic code execution
