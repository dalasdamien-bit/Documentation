# ⚙️ Askama #[template(...)] Attribute Reference

The `#[derive(Template)]` macro configures code generation using sub-attributes passed to `#[template(...)]`.

---

## 📋 Attribute Cheat-Sheet

| Sub-Attribute | Example | Description |
| :--- | :--- | :--- |
| `path` | `path = "home.html"` | Path to template relative to `templates/`. Cannot pair with `source`. |
| `source` | `source = "Hi {{ name }}"` | Inline template string. Requires `ext`. Cannot pair with `path`. |
| `ext` | `ext = "html"` | File extension hint for content-type and default escaping mode. |
| `block` | `block = "header"` | Renders only a single named block fragment from the file. |
| `blocks` | `blocks = ["title", "body"]` | Generates subtemplate helper methods like `tpl.as_title()`. |
| `escape` | `escape = "none"` | Override auto-escaping mode (`html` or `none`). |
| `whitespace` | `whitespace = "suppress"` | Override whitespace policy (`preserve`, `suppress`, `minimize`). |
| `print` | `print = "code"` | Debug print compiler output (`none`, `ast`, `code`, `all`). |
| `syntax` | `syntax = "custom"` | Select a custom syntax configuration from `askama.toml`. |
| `config` | `config = "askama.toml"` | Custom config file path relative to crate root. |
| `in_doc` | `in_doc = true` | Use the struct's docstrings as the template source code. |

---

## 🎯 Block Fragments & Partial Rendering

You can render individual template blocks without creating separate template files:

```rust
#[derive(Template)]
#[template(
    ext = "txt",
    source = "{% block title %}{{ title }}{% endblock %} {% block body %}{{ message }}{% endblock %}",
    blocks = ["title", "body"]
)]
struct Article<'a> {
    title: &'a str,
    message: &'a str,
}

let article = Article { title: "News", message: "Hello world" };

// Render just the title block!
assert_eq!(article.as_title().render().unwrap(), "News");
```

---

## 🔀 Templating Rust Enums

Askama supports deriving `Template` directly on `enum`s in two ways:

### Method A: Single Outer Template
```rust
#[derive(Template)]
#[template(path = "area.txt")]
enum Area {
    Square(f32),
    Rectangle { a: f32, b: f32 },
}
```
In `area.txt`:
```jinja
{% match self %}
  {% when Self::Square(side) %}{{ side }}^2
  {% when Self::Rectangle { a, b } %}{{ a }} * {{ b }}
{% endmatch %}
```

### Method B: Variant-Level Templates
```rust
#[derive(Template)]
#[template(ext = "txt")]
enum Area {
    #[template(source = "{{self.0}}^2")]
    Square(f32),
    #[template(source = "{{a}} * {{b}}")]
    Rectangle { a: f32, b: f32 },
}
```

---

## 📖 Template Code in Docstrings (`in_doc = true`)

Enable feature `code-in-doc` in Cargo.toml, then put your template inside doc comments:

```rust
/// ```askama
/// <div>{{ name }}</div>
/// ```
#[derive(Template)]
#[template(ext = "html", in_doc = true)]
struct UserDoc<'a> {
    name: &'a str,
}
```
