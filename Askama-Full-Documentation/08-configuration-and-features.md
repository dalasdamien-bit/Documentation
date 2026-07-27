# ⚙️ Configuration (askama.toml) & Cargo Features

Customize template search paths, whitespace policies, delimiters, and feature flags.

---

## 📄 1. `askama.toml` Configuration File

Place `askama.toml` in your crate root (next to `Cargo.toml`):

```toml
[general]
# Search directories for templates (supports globs)
dirs = ["templates", "src/views/**"]

# Whitespace handling: "preserve" (default), "suppress", or "minimize"
whitespace = "preserve"

# Custom delimiter syntax definition
[[syntax]]
name = "custom"
block_start = "%{"
block_end = "}%"
expr_start = "${"
expr_end = "}"

# Custom Escaper for specific file extensions
[[escaper]]
path = "askama::filters::Text"
extensions = ["js", "json", "txt"]
```

---

## ✂️ Whitespace Modifiers Legend

| Modifier | Example | Effect |
| :--- | :--- | :--- |
| `-` (Suppress) | `{%- if ok -%}` | Removes ALL whitespace before/after tag |
| `+` (Preserve) | `{%+ if ok +%}` | Explicitly retains whitespace |
| `~` (Minimize) | `{%~ if ok ~%}` | Collapses whitespace down to a single space or newline |

---

## 📦 Cargo Feature Flags Matrix

```toml
[dependencies]
askama = { version = "0.14.0", features = ["serde_json", "code-in-doc"] }
```

| Feature Flag | Default Enabled? | Description |
| :--- | :--- | :--- |
| `default` | ✅ YES | Includes `config`, `derive`, `std`, `urlencode` |
| `serde_json` | ❌ NO | Enables `|json` filter via `serde_json` crate |
| `code-in-doc`| ❌ NO | Enables docstring templates (`in_doc = true`) |
| `alloc` | ✅ (via std) | Use in `#![no_std]` with an allocator |
| `std` | ✅ YES | Direct std IO rendering (`write_into`) |
