# jsonschema-tomarkdown

Turn JSON Schema files into clean, readable markdown documentation.

You've got a `schema.json`. Your teammates don't want to read raw JSON. This tool generates human-friendly markdown tables, nested property docs, constraint summaries, and examples — all from your existing schema.

## Install

```bash
npm install -g jsonschema-tomarkdown
```

Or just use it directly:

```bash
npx jsonschema-tomd schema.json
```

## Usage

```bash
# Print to stdout
jsonschema-tomd schema.json

# Write to file
jsonschema-tomd schema.json -o docs/schema.md

# Custom title
jsonschema-tomd schema.json --title "API Configuration" -o README.md
```

## What it generates

Given a schema like:

```json
{
  "type": "object",
  "required": ["name", "email"],
  "properties": {
    "name": { "type": "string", "description": "Full name", "minLength": 1 },
    "email": { "type": "string", "format": "email" },
    "role": { "type": "string", "enum": ["admin", "user"], "default": "user" }
  }
}
```

You get markdown like:

```markdown
# Schema Documentation

**Type:** `object`

## Properties

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `name` | string | ✅ |  | Full name |
| `email` | string | ✅ |  |  |
| `role` | string |  | `user` |  |
```

### Supported features

- **Property tables** — name, type, required, default, description
- **Constraints** — min/max, minLength/maxLength, pattern, uniqueItems, etc.
- **Enums & const** — rendered inline
- **$ref resolution** — local `#/definitions/...` and `#/$defs/...` pointers
- **Composition** — `allOf`, `anyOf`, `oneOf` with nested rendering
- **Arrays** — tuple validation (items array) and single-schema items
- **Nested objects** — recursively rendered with depth control
- **$defs / definitions** — documented in their own section
- **Examples** — pretty-printed JSON code blocks
- **Additional properties** — noted as allowed or forbidden
- **Deprecated fields** — marked with ⚠️

## Programmatic API

```js
const { generateMarkdown } = require('jsonschema-tomarkdown');

const md = generateMarkdown(schema, {
  title: 'My API Schema',
  maxDepth: 5,
});

console.log(md);
```

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `title` | string | schema.title or "Schema Documentation" | Document title |
| `maxDepth` | number | 10 | Max nesting depth for properties |

## Why?

Because schema files are for machines, not humans. Every team that uses JSON Schema needs this — API docs, config validation docs, form schemas, you name it.

### How it compares

| Tool | Deps | CLI | Programmatic | $ref Support | Composition |
|------|------|-----|-------------|-------------|------------|
| **jsonschema-tomarkdown** | **0** | ✅ | ✅ | ✅ Local | ✅ allOf/anyOf/oneOf |
| @adobe/jsonschema2md | 50+ | ✅ | ❌ | External only | Partial |
| manual docs | — | ❌ | ❌ | — | — |

Zero dependencies. Works with Node 18+. One file in, beautiful docs out.

## License

MIT
