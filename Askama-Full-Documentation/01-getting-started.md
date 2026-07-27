# 🚀 Askama Quickstart Guide

Askama compiles Jinja-like templates directly into Rust code at compile time, giving you **zero-cost rendering** and **complete type safety**.

---

## 📦 1. Installation

Add `askama` to your `Cargo.toml`:

```toml
[dependencies]
askama = "0.14.0"
```

---

## 📁 2. Directory Conventions

By default, Askama looks for template files in a directory named `templates` located in your crate root (next to `Cargo.toml`):

```text
my_project/
├── Cargo.toml
├── src/
│   └── main.rs
└── templates/
    └── hello.html   <-- Create your template file here!
```

---

## 📝 3. Write Your Template

Inside `templates/hello.html`:

```html
Hello, {{ name }}!
```

---

## 🦀 4. Define and Render in Rust

Inside `src/main.rs`:

```rust
use askama::Template;

#[derive(Template)]
#[template(path = "hello.html")]
struct HelloTemplate<'a> {
    name: &'a str,
}

fn main() {
    let hello = HelloTemplate { name: "world" };
    
    // Render returns Result<String, askama::Error>
    println!("{}", hello.render().unwrap());
}
```

---

## ✨ Feature Highlights
- **Zero Runtime Overhead**: Templates compile into raw Rust code.
- **Type-Checked**: Variables and types are verified at compile time by the Rust compiler.
- **UTF-8 Safe**: Templates must be valid UTF-8.
- **Works on Stable Rust**: No nightly compiler required.
