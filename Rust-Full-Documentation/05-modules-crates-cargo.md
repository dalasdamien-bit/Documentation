# 📁 Packages, Crates & The Module System

Organize large codebases with clear privacy boundaries, public APIs, and multi-crate workspaces.

---

## 📐 Terminology Map

- **Package**: A Cargo feature containing a `Cargo.toml` describing how to build one or more crates.
- **Crate**: A tree of modules producing a library (`src/lib.rs`) or binary (`src/main.rs`).
- **Module**: Defined with `mod`, controls code structure, scope, and privacy.

---

## 🔒 Privacy Rules Cheat-Sheet

- **Default Privacy**: All items (functions, structs, fields, modules) are **private** to parent modules by default.
- **`pub` Keyword**: Exposes items to ancestor modules and external crates.
- **Struct Fields**: Struct fields remain private even if the struct is `pub` unless each field is explicitly marked `pub`.
- **Enum Variants**: Making an enum `pub` automatically makes **all of its variants public**.

---

## 🌿 Path References

```rust
// Absolute path starting from crate root
crate::front_of_house::hosting::add_to_waitlist();

// Relative path starting from parent module
super::deliver_order();

// Bringing path into scope
use std::collections::HashMap;
use std::io::{self, Write}; // Nested paths
```

---

## 🏗️ Cargo Workspaces

Share a single `Cargo.lock` and output directory across multiple related packages:

```toml
# Top-level Cargo.toml
[workspace]
resolver = "3"
members = ["adder", "add_one"]
```
