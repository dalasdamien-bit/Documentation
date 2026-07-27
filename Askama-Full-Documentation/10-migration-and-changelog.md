# 🔄 Version Migration Guide (v0.11 ➔ v0.16)

Key breaking changes and migration steps when upgrading Askama.

---

## ⚠️ Upgrading to Askama v0.16

### 1. Uninitialized Variables require `decl` / `declare`
Variable declaration without an initial value MUST use `{% decl var %}`:

```jinja
{# ❌ BAD in v0.16 #}
{% let my_var %}

{# ✅ GOOD #}
{% decl my_var %}
```

---

## ⚠️ Upgrading to Askama v0.15

### 1. Custom Filters require `#[askama::filter_fn]`
Custom filter functions must be annotated with the macro and accept runtime values:

```rust
// ✅ Correct v0.15+ custom filter signature
#[askama::filter_fn]
pub fn my_filter(val: impl std::fmt::Display, _env: &dyn askama::Values) -> askama::Result<String> {
    Ok(val.to_string())
}
```

---

## 🔀 Rinja & Askama Reunification

Rinja and Askama have merged back into a single unified `askama` crate:
- Replace `use rinja::Template;` with `use askama::Template;`.
- Standalone integration crates (`askama_axum`, `rinja_axum`) are replaced by direct `template.render()` calls.
