# 🧪 Askama Filters Reference

Filters transform template expressions using the pipe symbol (`|`). Multiple filters can be chained together: `{{ text | trim | capitalize }}`.

---

## 📚 Built-In Filters Table

| Filter | Usage Example | Output |
| :--- | :--- | :--- |
| `capitalize` | `{{ "hello" | capitalize }}` | `"Hello"` |
| `center(w)` | `{{ "a" | center(5) }}` | `"  a  "` |
| `escape` / `e` | `{{ "<tag>" | e }}` | `"&lt;tag&gt;"` |
| `filesizeformat` | `{{ 1024 | filesizeformat }}` | `"1.02 KB"` |
| `fmt(str)` | `{{ val | fmt("{:?}") }}` | Formatted value |
| `format(args...)`| `{{ "{}" | format(name) }}` | Formatted string |
| `indent(n)` | `{{ text | indent(4) }}` | Indented lines |
| `join(sep)` | `{{ list | join(", ") }}` | `"a, b, c"` |
| `linebreaks` | `{{ text | linebreaks }}` | Replaces `\n` with `<br>` / `<p>` |
| `lower` | `{{ "HI" | lower }}` | `"hi"` |
| `pluralize` | `{{ count | pluralize("cat", "cats") }}` | Pluralized string |
| `safe` | `{{ raw_html | safe }}` | Disables HTML escaping |
| `title` | `{{ "hello world" | title }}` | `"Hello World"` |
| `trim` | `{{ " hi " | trim }}` | `"hi"` |
| `truncate(n)` | `{{ "long text" | truncate(4) }}` | `"long..."` |
| `unique` | `{{ list | unique }}` | Unique items iterator |
| `upper` | `{{ "hi" | upper }}` | `"HI"` |
| `urlencode` | `{{ "a b?" | urlencode }}` | `"a%20b%3F"` |

---

## 📦 JSON Serialization Filter (`json` / `tojson`)

Enable feature `serde_json` in Cargo.toml to enable:

```jinja
<script>
  // Safe embedded JSON object
  var config = {{ app_config | json | safe }};
  // Pretty-printed JSON with 2 spaces indentation
  var pretty = {{ app_config | json(2) | safe }};
</script>
```

---

## 🛠️ Writing Custom Filters (`#[askama::filter_fn]`)

Custom filters require the `#[askama::filter_fn]` proc-macro and must take `_env: &dyn askama::Values` as their second argument:

```rust
use askama::Template;

#[derive(Template)]
#[template(source = "{{ text | slugify }}", ext = "txt")]
struct PostTemplate<'a> {
    text: &'a str,
}

mod filters {
    #[askama::filter_fn]
    pub fn slugify(
        value: impl std::fmt::Display,
        _env: &dyn askama::Values,
    ) -> askama::Result<String> {
        let slug = value.to_string()
            .to_lowercase()
            .replace(' ', "-");
        Ok(slug)
    }
}
```
