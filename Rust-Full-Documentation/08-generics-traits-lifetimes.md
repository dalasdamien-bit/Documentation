# 🧬 Generic Types, Traits & Lifetimes

Tools for abstracting duplicate code while maintaining total type safety and zero runtime overhead.

---

## 📦 1. Generic Data Types

Rust uses **Monomorphization** at compile time: converting generic code into specific concrete types, incurring **zero performance cost**.

```rust
struct Point<T, U> {
    x: T,
    y: U,
}
```

---

## 🎨 2. Traits & Trait Bounds

Traits define shared interface behavior across types.

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}

// Function taking any type implementing Summary
pub fn notify(item: &impl Summary) { ... }

// Trait Bound Syntax with 'where' clause
fn process<T, U>(t: &T, u: &U)
where
    T: Summary + std::fmt::Display,
    U: Clone + std::fmt::Debug,
{ ... }
```

---

## ⌛ 3. Lifetimes (`'a`)

Lifetimes prevent **dangling references** by ensuring references remain valid as long as needed.

```rust
// Explicit lifetime annotation: returned reference lives as long as the smaller parameter lifetime
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() { x } else { y }
}

// Struct holding a reference
struct ImportantExcerpt<'a> {
    part: &'a str,
}

// 'static lifetime: Valid for the entire duration of the program (e.g. string literals)
let s: &'static str = "I live forever";
```

---

### 🔍 The 3 Lifetime Elision Rules (Automatic Inference)
1. Each reference parameter gets its own lifetime parameter.
2. If there is exactly one input lifetime, it is assigned to all output lifetimes.
3. If one parameter is `&self` or `&mut self`, its lifetime is assigned to all output lifetimes.
